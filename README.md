# Shopify theme deploy actions

Deploy live/test themes, and backup theme configs.

## Task
The theme developer needs to test and maintain the theme code on multiple stores. Each store has unique theme settings.

The example configuration is built for six stores. Store 0 - has a default theme settings. Used to generate the release ZIP package to distribute via the Shopify theme store. Store 1-5 - Shopify theme store allows up to five theme demo stores.

Use the **Deploy test** action, to upload the prerelease theme version merged with live theme settings. Useful for test themes on various configurations.

Use **Deploy live** action, to push tested, approved theme version to live, and generate the theme ZIP file for distribution.

Use **Backup** action, to create a backup copy of the live theme configuration files.

## Actions

### Backup

```
.github / workflows / backup.yaml
```

Steps:
- pull theme settings from the live theme
- zip
- save as workflow artifact

Scheduled to run once per week.

### Deploy live

```
.github / workflows / deploy-live.yaml
```

Wrapper for ```shopify theme push``` command.

Create a tag with a "release" prefix to trigger this action.

### Deploy test

```
.github / workflows / deploy-test.yaml
```

Deploy test theme & merge live theme config, more details - https://github.com/alexanderlukjanenko/deploy-and-copy-configs

Create a tag with a "test" prefix to trigger this action.

## Variables
### **BACKUP_FILES** 
List of configuration files to copy. Using the **--only** flag for ```shopify theme pull``` command. \
Example: --only templates/\*.json --only config/\* --only sections/\*.json

### **CONFIG_FILES** 
List of configuration files to merge during test deploy. \
Example: --only templates/\*.json --only sections/\*.json --only config/settings_data.json

### **IGNORE_FILES** 
List of configuration files to ignore during live deploy. Using the **--ignore** flag for ```shopify theme push``` command. \
Example: --ignore config/settings_data.json --ignore templates/\*.json --ignore sections/\*.json --ignore snippets/svg-logo.liquid --ignore config.yml

### **STORE_0_NAME** 
Short name for the store. Add the same variable per each store: STORE_1_NAME, STORE_2_NAME, STORE_3_NAME, STORE_4_NAME, STORE_5_NAME. \
Example: Default

### **STORE_0_URL** 
Store URL, like your-store.myshopify.com. Add the same variable per each store: STORE_1_URL, STORE_2_URL, STORE_3_URL, STORE_4_URL, STORE_5_URL \
Example: your-store.myshopify.com

## Secrets
### **STORE_0_PASSWORD** 
Password generated from Theme Access app. More details about the Theme Access app - https://shopify.dev/docs/themes/tools/theme-access. Add the same variable per each store: STORE_1_PASSWORD, STORE_2_PASSWORD, STORE_3_PASSWORD, STORE_4_PASSWORD, STORE_5_PASSWORD. \
Example: shptka_dd99999d9999aa555555555c777c2222


## License

This repository is licensed under the MIT license. See the [LICENSE.md](LICENSE.md) file for details.
