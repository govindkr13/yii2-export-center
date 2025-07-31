# Yii2 Export Center Module

A modular and extensible export system for Yii2 Advanced Template projects. It supports various data export strategies (CSV, Excel, PDF) and can switch to background processing via queue when handling large datasets.

---

## 📦 Features

- Plug-and-play Export Strategy system (CSV, Excel, etc.)
- Chunked export processing to handle large datasets efficiently
- Console and Web export trigger support
- Export queue integration with `yii2-queue`
- Logs who exported what, when, and in which format
- Easily extendable for any model or export format

---

## 🏗️ Installation

1. **Extract the module** under your Yii2 advanced app:

```
common/modules/export/
```

2. **Run the migration** to create the `export_log` table:

```bash
php yii migrate --migrationPath=@common/modules/export/migrations
```

3. **Register the export strategy** in your `bootstrap.php`:

```php
Yii::$container->setSingleton('exportCenter', function () {
    $center = new \common\modules\export\components\ExportCenter();
    $center->registerStrategy('csv', new \common\modules\export\components\strategies\CsvExport());
    return $center;
});
```

---

## 🚀 Usage

### ✅ Web Trigger

```
GET /export/export?handler=user&format=csv
```

### ✅ Console Command

```bash
php yii export/run user csv --filters='{"status":1}'
```

---

## 📂 Directory Structure

```
components/
    ExportCenter.php
    strategies/
        CsvExport.php
handlers/
    BaseExportHandler.php
    UserExportHandler.php
    TransactionExportHandler.php
    LoanRequestExportHandler.php
jobs/
    ExportJob.php
models/
    ExportLog.php
commands/
    ExportController.php
controllers/
    ExportController.php
migrations/
    m240730_123456_create_export_log_table.php
```

---

## ✏️ Creating a New Handler

1. Extend the `BaseExportHandler` class.
2. Implement the `getQuery()` and `formatRow()` methods.
3. Register and trigger it like this:

```bash
php yii export/run my-new-handler csv
```

---

## 🧰 Planned Extensions

- [ ] Excel (XLSX) export support
- [ ] PDF export support
- [ ] UI for export logs and download history
- [ ] Notifications on export completion (via Lark/Email)

---

## 🤝 Contributing

PRs and forks are welcome. If you'd like to contribute or report issues, feel free to open an issue or contact [govindkr13](https://github.com/govindkr13).

---

## 📜 License

MIT License – use freely in commercial and personal projects.
