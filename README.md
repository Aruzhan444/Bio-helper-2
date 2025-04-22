from pathlib import Path

# Создание структуры проекта
project_path = Path("/mnt/data/bio-helper")
project_path.mkdir(parents=True, exist_ok=True)

# Содержимое файлов
index_html = """
<!DOCTYPE html>
<html lang="kk">
<head>
  <meta charset="UTF-8">
  <title>Биология көмекшісі</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Биология пәнінен көмек</h1>
  <input type="text" id="searchInput" placeholder="Мысалы: митоз, ДНҚ, өсімдіктер...">
  <div id="results"></div>

  <script src="script.js"></script>
</body>
</html>
"""

style_css = """
body {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
}
input {
  width: 60%;
  padding: 10px;
  font-size: 16px;
}
#results {
  margin-top: 20px;
  text-align: left;
}
"""

script_js = """
const data = {
  "митоз": "Митоз – жасушаның бөліну процесі. Бұл процесс 5 кезеңнен тұрады...",
  "днқ": "ДНҚ – тұқымқуалаушылық ақпаратты тасымалдайтын молекула...",
  "хлоропласт": "Хлоропласт – фотосинтез жүретін органелла..."
};

document.getElementById('searchInput').addEventListener('input', function() {
  const query = this.value.toLowerCase();
  const resultDiv = document.getElementById('results');
  resultDiv.innerHTML = data[query] ? `<p>${data[query]}</p>` : '<p>Материал табылмады.</p>';
});
"""

# Запись файлов
(index_path := project_path / "index.html").write_text(index_html, encoding="utf-8")
(style_path := project_path / "style.css").write_text(style_css, encoding="utf-8")
(script_path := project_path / "script.js").write_text(script_js, encoding="utf-8")

# Упаковка в архив
archive_path = Path("/mnt/data/bio-helper.zip")
import shutil
shutil.make_archive(str(archive_path).replace('.zip', ''), 'zip', project_path)

archive_path.name
