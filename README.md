# 📘 Local Link Checker for Text-Based Files

This Python script validates whether specified "broken link" strings exist within local **text-based files** (e.g., `.md`, `.yml`, `.json`, `.txt`) that are referenced via GitHub blob URLs.

It is designed for documentation maintainers and contributors who want to quickly verify if broken links have been correctly fixed in local clones of GitHub repositories.

---

## 🔧 What It Does

- Reads an Excel file (`Invalid-link-check.xlsx`) that includes:
  - A **broken link ID** (text snippet to search for)
  - A **GitHub blob-style URL** to a file (e.g., markdown, YAML)
- Converts the GitHub blob URL into a local file path (based on a configured local repository root folder)
- Opens the file and checks if it contains the specified text
- Outputs a formatted Excel file with a result column:
  - ✅ **If found** → leaves the cell empty
  - ❌ **If not found** → marks as `NF` (Not Found)
  - 📁 Reports issues like invalid URL, file not found, or read error
- Beautifies the Excel file:
  - Applies the `DengXian` font (11pt)
  - Auto-adjusts column widths
- Automatically opens the Excel file upon completion

---

## 📂 Folder & File Structure

- **Input**: Excel file named `Invalid-link-check.xlsx` located on your **Desktop**
- **Output**: A timestamped Excel file saved under a new folder:

```yaml
Desktop/
 └── Link-checker/
     └── Check_Result_YYYY-MM-DD_HH-MM-SS.xlsx
```

---

## 📝 Input Format: `Invalid-link-check.xlsx`

Must include **two columns** with the following exact headers:

| Broken link ID      | Source URL                                                   |
| ------------------- | ------------------------------------------------------------ |
| `/docs/intro`       | https://github.com/your-org/your-repo/blob/main/docs/example.md |
| `some: yaml: entry` | https://github.com/your-org/your-repo/blob/main/config/settings.yml |

---

## 📤 Output Format

The script adds a new column `Check Result` with one of the following values:

| Broken link ID | Source URL | Check Result             |
| -------------- | ---------- | ------------------------ |
| `/docs/intro`  | ...        | *(empty = match found)*  |
| `some-id`      | ...        | `NF`                     |
| ...            | ...        | `File not found locally` |
| ...            | ...        | `Read failed`            |

---

## ⚙️ Configuration

Update this line in the script to point to the root folder containing your local GitHub repositories:

```python
SEARCH_ROOT = r'C:\Projects'
```

Make sure the file structure in your local repo matches the paths in the `Source URL` column (usually corresponds to the `main` branch on GitHub).

---

## ✅ Requirements

- Python 3.7 or higher
- Install dependencies via pip:

```bash
pip install pandas openpyxl
```

---

## ▶️ How to Use

1. Save your input Excel file as `Invalid-link-check.xlsx` on your **Desktop**
2. Ensure your local repositories are up-to-date (e.g., on the `main` branch)
3. Run the script in your Python environment
4. Once complete:
   - A formatted Excel file is saved in `~/Desktop/Link-checker/`
   - The file opens automatically

---

## 💡 Notes

- Supports any text-based file (`.md`, `.yml`, `.json`, `.txt`, etc.)
- Does **not** parse structured formats (e.g., YAML keys) — checks are plain-text search
- Only supports GitHub-style blob links: `https://github.com/.../blob/branch/path/to/file.ext`
- Assumes file structure in your local repo matches the branch and paths in the URL

---

## 📄 License

Internal use only. You are free to adapt this script to your team's documentation workflow.
