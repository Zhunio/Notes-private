# SuiteCloud Setup Build/Deploy GitHub Actions

## Prerequisites

- [SuiteCloud CLI for Node.js](https://www.npmjs.com/package/@oracle/suitecloud-cli)

## 1. Enable Features

- Go to **Setup** → **Company** → **Enable Features** → **SuiteCloud**
- Enable:
  - **Client SuiteScript**
  - **Server SuiteScript**
  - **OAuth 2.0**
  - **Suitecloud Development Framework (SDF)**

## 2. Create Certificate

1. Create Certificate

```bash
openssl req -new -x509 -newkey rsa:4096 -sha256 \
-sigopt rsa_padding_mode:pss \
-sigopt rsa_pss_saltlen:64 \
-keyout suitecloud_key.pem \
-out suitecloud_cert.pem \
-nodes
```

> [!NOTE]
> Keep `suitecloud_cert.pem` and `suitecloud_key.pem` handy for next steps.

## 3. Upload Certificate

- Go to **Setup** → **Integration** → **OAuth 2.0 Client Credentials (M2M) Setup**
- Create New:
  - Entity: Administrator (or specific user)
  - Role: Administrator
  - Application: SuiteCloud Development Integration
  - Certificate: Upload `suitecloud_cert.pem`
  - Save
- Copy **Certificate ID**

> [!NOTE]
> Keep `Certificate ID` handy for next steps.

## 4. Set Environment Variables

```bash
export SUITECLOUD_ACCOUNT=          # NetSuite Account ID (e.g., 1234567_SB1)
export SUITECLOUD_AUTHID=           # Can be any identifier (e.g. ci)
export SUITECLOUD_CERTIFICATE_ID=   # Certificate ID
export SUITECLOUD_PRIVATE_KEY_PATH= # Path to `suitecloud_key.pem`

export SUITECLOUD_CI_PASSKEY=       # 32-100 alphanumeric password used by SuiteCloud CLI to generate the ~/.suitecloud-sdk/credentials_ci.p12 file
```

> [!NOTE]
> Keep the `SUITECLOUD_CI_PASSKEY`

## 5. Run the `suitecloud account:setup:ci` Command

```bash
suitecloud account:setup:ci \
--account $SUITECLOUD_ACCOUNT \
--authid $SUITECLOUD_AUTHID \
--certificateid $SUITECLOUD_CERTIFICATE_ID \
--privatekeypath $SUITECLOUD_PRIVATE_KEY_PATH
```

> [!NOTE]
> This command generates the `~/.suitecloud-sdk/credentials\_<authid>.p12

## 6. Run the `suitecloud project:validate --server` Command

```bash
export SUITECLOUD_CI=1
suitecloud project:validate --server
```

> [!NOTE]
> We need to set the `SUITECLOUD_CI` environment variable to `1` to indicate that we are running in a CI environment.

## 7. Create Repository Secrets for Build/Deploy GHA Workflows

- Go to your GitHub repository
- Click on **Settings** → **Secrets and variables** → **Actions**
- Add the following repository secrets:
  - `SUITECLOUD_AUTHID`
  - `SUITECLOUD_CERTIFICATE_ID`
  - `SUITECLOUD_PRIVATE_KEY` (with the content of `suitecloud_key.pem`)
  - `SUITECLOUD_PRIVATE_KEY_PATH`
  - `SUITECLOUD_CI_PASSKEY`

## 8. Create Environments for Build/Deploy GHA Workflows

- Go to your GitHub repository
- Click on **Settings** → **Environments**
- Create two environments: `sandbox` and `production`
- For each environment, add the following environment secret:
  - `SUITECLOUD_ACCOUNT` (with the respective Account ID)

## 9. Update `package.json` scripts/devDependencies

```json
{
  "scripts": {
    "suitecloud:account:setup:ci": "suitecloud account:setup:ci --account $SUITECLOUD_ACCOUNT --authid $SUITECLOUD_AUTHID --certificateid $SUITECLOUD_CERTIFICATE_ID --privatekeypath $SUITECLOUD_PRIVATE_KEY_PATH",
    "suitecloud:project:validate": "suitecloud project:validate --server",
    "suitecloud:project:deploy": "suitecloud project:deploy"
  },
  "devDependencies": {
    "@oracle/suitecloud-cli": "^3.1.2"
  }
}
```

## 10. Create Build GHA Workflow

```yaml
# .github/workflows/build.yml
name: Build

on: pull_request

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    environment: ${{ github.base_ref == 'main' && 'production' || 'sandbox' }}
    env:
      SUITECLOUD_ACCOUNT: ${{ secrets.SUITECLOUD_ACCOUNT }}
      SUITECLOUD_AUTHID: ${{ secrets.SUITECLOUD_AUTHID }}
      SUITECLOUD_CERTIFICATE_ID: ${{ secrets.SUITECLOUD_CERTIFICATE_ID }}
      SUITECLOUD_PRIVATE_KEY: ${{ secrets.SUITECLOUD_PRIVATE_KEY }}
      SUITECLOUD_PRIVATE_KEY_PATH: ${{ secrets.SUITECLOUD_PRIVATE_KEY_PATH }}
      SUITECLOUD_CI_PASSKEY: ${{ secrets.SUITECLOUD_CI_PASSKEY }}
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: "22.x"
          cache: "npm"

      - name: Install dependencies
        run: npm ci --acceptsuitecloudsdklicense

      - name: SuiteCloud Copy Private Key
        run: echo -e "$SUITECLOUD_PRIVATE_KEY" > $SUITECLOUD_PRIVATE_KEY_PATH

      - name: SuiteCloud Setup Account
        run: npm run suitecloud:account:setup:ci

      - name: SuiteCloud Validate Project
        env:
          SUITECLOUD_CI: 1
        run: npm run suitecloud:project:validate
```

## 11. Create Deploy GHA Workflow

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Select the deployment environment"
        required: true
        default: "sandbox"
        type: choice
        options:
          - sandbox
          - production

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    environment: ${{ inputs.environment }}
    env:
      SUITECLOUD_ACCOUNT: ${{ secrets.SUITECLOUD_ACCOUNT }}
      SUITECLOUD_AUTHID: ${{ secrets.SUITECLOUD_AUTHID }}
      SUITECLOUD_CERTIFICATE_ID: ${{ secrets.SUITECLOUD_CERTIFICATE_ID }}
      SUITECLOUD_PRIVATE_KEY: ${{ secrets.SUITECLOUD_PRIVATE_KEY }}
      SUITECLOUD_PRIVATE_KEY_PATH: ${{ secrets.SUITECLOUD_PRIVATE_KEY_PATH }}
      SUITECLOUD_CI_PASSKEY: ${{ secrets.SUITECLOUD_CI_PASSKEY }}
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: "22.x"
          cache: "npm"

      - name: Install dependencies
        run: npm ci --acceptsuitecloudsdklicense

      - name: SuiteCloud Copy Private Key
        run: echo -e "$SUITECLOUD_PRIVATE_KEY" > $SUITECLOUD_PRIVATE_KEY_PATH

      - name: SuiteCloud Setup Account
        run: npm run suitecloud:account:setup:ci

      - name: SuiteCloud Deploy Project
        env:
          SUITECLOUD_CI: 1
        run: npm run suitecloud:project:deploy
```
