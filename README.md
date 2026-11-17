
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#211632">
  <meta name="description" content="Lunaria: un pequeño universo donde siempre hay un lugar para ti.">
  <link rel="manifest" href="./manifest.json">
  <title>Lunaria 🌙</title>

  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: Georgia, serif;
      color: #f8f1ff;
      background: linear-gradient(150deg, #171126, #38264e, #72558c);
    }

    button, input, textarea, select { font: inherit; }

    button {
      border: 1px solid #d9c4f0;
      border-radius: 25px;
      padding: 12px 20px;
      color: white;
      background: #ffffff20;
      cursor: pointer;
    }

    button:active { transform: scale(.98); }

    button:disabled { opacity: .45; cursor: not-allowed; }

    .app {
      width: 100%;
      max-width: 760px;
      min-height: 100vh;
      margin: auto;
      padding: 24px 18px 50px;
    }

    header { text-align: center; padding: 15px 0 25px; }

    .moon {
      font-size: 58px;
      animation: glow 3s infinite alternate;
    }

    h1 {
      margin: 8px 0;
      font-size: 2.8rem;
      font-weight: normal;
      letter-spacing: 5px;
    }

    .subtitle { color: #e3d2f5; font-style: italic; }

    nav {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 9px;
      margin: 20px 0 30px;
    }

    nav button { padding: 10px 15px; }

    .panel {
      padding: 22px;
      border: 1px solid #ffffff35;
      border-radius: 22px;
      background: #ffffff12;
      box-shadow: 0 12px 35px #10091c45;
    }

    h2 { font-weight: normal; color: #ead9ff; }

    .welcome { text-align: center; padding: 28px 12px; }

    .welcome p { line-height: 1.9; }

    .field { margin: 17px 0; text-align: left; }

    label {
      display: block;
      margin-bottom: 8px;
      color: #ead9ff;
    }

    input, textarea, select {
      width: 100%;
      padding: 13px;
      border: 1px solid #d8c2ec70;
      border-radius: 12px;
      color: white;
      background: #211632;
      outline: none;
    }

    textarea { min-height: 180px; resize: vertical; line-height: 1.7; }

    input::placeholder, textarea::placeholder { color: #c5b3d4; }

    .primary {
      background: #a184c1;
      border-color: #cdb6e8;
      color: #211632;
      font-weight: bold;
    }

    .book {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      margin: 12px 0;
      padding: 15px;
      border: 1px solid #ffffff30;
      border-radius: 15px;
      background: #ffffff12;
    }

    .book-info { min-width: 0; }
    .book-info strong { display: block; overflow-wrap: anywhere; }
    .book-info small { color: #d8c8e8; }

    .book-actions { display: flex; flex-wrap: wrap; gap: 7px; }
    .book-actions button { padding: 8px 12px; }

    .reader-title { text-align: center; }

    .reader {
      margin-top: 20px;
      padding: 20px;
      border-radius: 16px;
      background: #f5edfa;
      color: #342342;
      text-align: left;
      line-height: 2;
      font-size: 1.08rem;
      white-space: normal;
      overflow-wrap: anywhere;
    }

    .reader p { margin: 0 0 20px; }
    .reader p.reading {
      background: #e5d3f5;
      border-radius: 8px;
      outline: 5px solid #e5d3f5;
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 9px;
      margin: 18px 0;
    }

    .hint {
      color: #ddcce9;
      font-size: .9rem;
      line-height: 1.6;
    }

    .hidden { display: none !important; }

    footer {
      margin-top: 35px;
      color: #d6c4e7;
      text-align: center;
      font-size: .9rem;
    }

    @keyframes glow {
      to {
        text-shadow: 0 0 28px #fff, 0 0 45px #c9a8f2;
        transform: scale(1.08);
      }
    }

    @media (max-width: 480px) {
      .app { padding-left: 13px; padding-right: 13px; }
      h1 { font-size: 2.3rem; }
      .panel { padding: 17px; }
      .book { align-items: flex-start; flex-direction: column; }
    }
  </style>
</head>

<body>
  <div class="app">
    <header>
      <div class="moon">☾</div>
      <h1>Lunaria</h1>
      <p class="subtitle">Un pequeño universo donde siempre hay un lugar para ti.</p>
    </header>

    <nav>
      <button onclick="showSection('home')">Inicio</button>
      <button onclick="showSection('library')">Mi biblioteca</button>
      <button onclick="showSection('add')">Añadir libro</button>
    </nav>

    <section id="home" class="panel welcome">
      <h2>Bienvenida a casa ✨</h2>
      <p>
        Hay historias que nos encuentran cuando más las necesitamos.
        Este pequeño rincón es tuyo: para leer, imaginar y perderte
        un ratito entre palabras.
      </p>
      <button class="primary" onclick="showSection('library')">Entrar a mi biblioteca</button>
      <p class="hint">Que nunca te falten historias ni estrellas.</p>
      <button id="install" class="hidden">Instalar Lunaria 🌙</button>
    </section>

    <section id="library" class="panel hidden">
      <h2>Mi biblioteca ✧</h2>
      <p class="hint">Tus historias guardadas en este dispositivo.</p>
      <div id="bookList"></div>
      <p id="emptyMessage" class="hint">Todavía no hay libros. Puedes añadir el primero cuando quieras. 💜</p>
    </section>

    <section id="add" class="panel hidden">
      <h2>Un nuevo universo 📖</h2>
      <form id="bookForm">
        <div class="field">
          <label for="bookTitle">Título del libro</label>
          <input id="bookTitle" required maxlength="120" placeholder="El nombre de tu historia">
        </div>
        <div class="field">
          <label for="bookAuthor">Autor</label>
          <input id="bookAuthor" maxlength="120" placeholder="Nombre del autor">
        </div>
        <div class="field">
          <label for="bookContent">Contenido del libro</label>
          <textarea id="bookContent" required placeholder="Pega aquí el texto de tu libro..."></textarea>
        </div>
        <button class="primary" type="submit">Guardar en mi biblioteca ✨</button>
      </form>
      <p class="hint">Por ahora puedes pegar el texto del libro. Se guardará en este navegador.</p>
    </section>

    <section id="reading" class="panel hidden">
      <div class="reader-title">
        <h2 id="readingTitle">Mi lectura</h2>
        <p id="readingAuthor" class="hint"></p>
      </div>

      <div class="field">
        <label for="voiceSelect">Voz de lectura</label>
        <select id="voiceSelect">
          <option value="">Buscando voces disponibles...</option>
        </select>
        <p class="hint">
          Las voces dependen de las que tu Android y navegador tengan instaladas.
          Elige la que más te guste.
        </p>
      </div>

      <div class="field">
        <label for="speedSelect">Velocidad de lectura</label>
        <select id="speedSelect">
          <option value="0.75">Lenta</option>
          <option value="0.88" selected>Tranquila</option>
          <option value="1">Normal</option>
          <option value="1.15">Rápida</option>
        </select>
      </div>

      <div class="controls">
        <button onclick="speakBook()">▶ Leer</button>
        <button onclick="pauseBook()">Ⅱ Pausar</button>
        <button onclick="resumeBook()">▶ Continuar</button>
        <button onclick="stopBook()">■ Detener</button>
      </div>

      <div id="reader" class="reader"></div>

      <div class="controls">
        <button onclick="showSection('library')">Volver a mi biblioteca</button>
      </div>
    </section>

    <footer>Hecho de sueños, palabras y un poquito de magia. 🌙</footer>
  </div>

  <script>
    const STORAGE_KEY = "lunariaBooks";
    let books = [];
    let currentBook = null;
    let currentParagraph = 0;
    let utterance = null;
    let availableVoices = [];
    let readingSession = 0;

    function loadBooks() {
      try {
        books = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
        if (!Array.isArray(books)) books = [];
      } catch (error) {
        books = [];
      }
      renderBooks();
    }

    function saveBooks() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(books));
      renderBooks();
    }

    function showSection(section) {
      stopBook();
      ["home", "library", "add", "reading"].forEach(id => {
        document.getElementById(id).classList.toggle("hidden", id !== section);
      });

      if (section === "library") renderBooks();
    }

    document.getElementById("bookForm").addEventListener("submit", event => {
      event.preventDefault();

      const title = document.getElementById("bookTitle").value.trim();
      const author = document.getElementById("bookAuthor").value.trim();
      const content = document.getElementById("bookContent").value.trim();

      if (!title || !content) {
        alert("Escribe al menos el título y el contenido del libro.");
        return;
      }

      books.push({
        id: Date.now().toString(),
        title,
        author,
        content
      });

      saveBooks();
      event.target.reset();
      showSection("library");
      alert("Tu libro ya forma parte de Lunaria. 💜");
    });

    function renderBooks() {
      const list = document.getElementById("bookList");
      const empty = document.getElementById("emptyMessage");
      list.innerHTML = "";
      empty.classList.toggle("hidden", books.length > 0);

      books.forEach(book => {
        const item = document.createElement("div");
        item.className = "book";

        const info = document.createElement("div");
        info.className = "book-info";

        const title = document.createElement("strong");
        title.textContent = book.title;

        const author = document.createElement("small");
        author.textContent = book.author || "Autor desconocido";

        info.append(title, author);

        const actions = document.createElement("div");
        actions.className = "book-actions";

        const open = document.createElement("button");
        open.textContent = "Leer";
        open.addEventListener("click", () => openBook(book.id));

        const remove = document.createElement("button");
        remove.textContent = "Eliminar";
        remove.addEventListener("click", () => deleteBook(book.id));

        actions.append(open, remove);
        item.append(info, actions);
        list.appendChild(item);
      });
    }

    function openBook(id) {
      const book = books.find(item => item.id === id);
      if (!book) return;

      stopBook();
      currentBook = book;
      currentParagraph = 0;

      document.getElementById("readingTitle").textContent = book.title;
      document.getElementById("readingAuthor").textContent =
        book.author || "Autor desconocido";

      const reader = document.getElementById("reader");
      reader.innerHTML = "";

      const paragraphs = book.content.split(/\n+/).filter(p => p.trim());

      paragraphs.forEach((text, index) => {
        const paragraph = document.createElement("p");
        paragraph.id = "paragraph-" + index;
        paragraph.textContent = text;
        reader.appendChild(paragraph);
      });

      showSection("reading");
    }

    function deleteBook(id) {
      if (!confirm("¿Quieres eliminar este libro de tu biblioteca?")) return;
      stopBook();
      books = books.filter(book => book.id !== id);
      if (currentBook && currentBook.id === id) currentBook = null;
      saveBooks();
    }

    function loadVoices() {
      if (!("speechSynthesis" in window)) return;

      availableVoices = speechSynthesis.getVoices();
      const selector = document.getElementById("voiceSelect");
      if (!selector) return;

      const previous = localStorage.getItem("lunariaVoice") || selector.value;

      selector.innerHTML = "";

      if (!availableVoices.length) {
        const option = document.createElement("option");
        option.value = "";
        option.textContent = "No se encontraron voces todavía";
        selector.appendChild(option);
        return;
      }

      const sortedVoices = [...availableVoices].sort((a, b) => {
        const aSpanish = a.lang.toLowerCase().startsWith("es") ? 0 : 1;
        const bSpanish = b.lang.toLowerCase().startsWith("es") ? 0 : 1;
        return aSpanish - bSpanish || a.name.localeCompare(b.name);
      });

      sortedVoices.forEach(voice => {
        const option = document.createElement("option");
        option.value = voice.name;
        option.textContent = voice.name + " — " + voice.lang;
        selector.appendChild(option);
      });

      if (sortedVoices.some(voice => voice.name === previous)) {
        selector.value = previous;
      } else {
        const spanishVoice = sortedVoices.find(voice =>
          voice.lang.toLowerCase().startsWith("es")
        );
        if (spanishVoice) selector.value = spanishVoice.name;
      }
    }

    document.getElementById("voiceSelect").addEventListener("change", event => {
      localStorage.setItem("lunariaVoice", event.target.value);
    });

    function speakBook() {
      if (!currentBook) return;

      if (!("speechSynthesis" in window)) {
        alert("Tu navegador no admite lectura en voz alta.");
        return;
      }

      speechSynthesis.cancel();
      readingSession++;
      currentParagraph = 0;
      readNext(readingSession);
    }

    function readNext(session) {
      if (!currentBook || session !== readingSession) return;

      const paragraphs = currentBook.content
        .split(/\n+/)
        .filter(p => p.trim());

      if (currentParagraph >= paragraphs.length) {
        stopBook();
        return;
      }

      document.querySelectorAll(".reader p").forEach(p => {
        p.classList.remove("reading");
      });

      const element = document.getElementById("paragraph-" + currentParagraph);

      if (element) {
        element.classList.add("reading");
        element.scrollIntoView({ behavior: "smooth", block: "center" });
      }

      utterance = new SpeechSynthesisUtterance(paragraphs[currentParagraph]);

      const selectedName = document.getElementById("voiceSelect").value;
      const selectedVoice = availableVoices.find(v => v.name === selectedName);

      if (selectedVoice) {
        utterance.voice = selectedVoice;
        utterance.lang = selectedVoice.lang;
      } else {
        utterance.lang = "es";
      }

      utterance.rate = Number(document.getElementById("speedSelect").value) || 0.88;
      utterance.pitch = 0.95;
      utterance.volume = 1;

      utterance.onend = () => {
        if (session !== readingSession) return;
        currentParagraph++;
        readNext(session);
      };

      utterance.onerror = () => {
        if (session !== readingSession) return;
        currentParagraph++;
        readNext(session);
      };

      speechSynthesis.speak(utterance);
    }

    function pauseBook() {
      if ("speechSynthesis" in window && speechSynthesis.speaking) {
        speechSynthesis.pause();
      }
    }

    function resumeBook() {
      if ("speechSynthesis" in window && speechSynthesis.paused) {
        speechSynthesis.resume();
      }
    }

    function stopBook() {
      readingSession++;
      if ("speechSynthesis" in window) speechSynthesis.cancel();
      document.querySelectorAll(".reader p").forEach(p => {
        p.classList.remove("reading");
      });
    }

    if ("speechSynthesis" in window) {
      loadVoices();
      speechSynthesis.onvoiceschanged = loadVoices;
    } else {
      document.getElementById("voiceSelect").innerHTML =
        '<option value="">Lectura no disponible en este navegador</option>';
    }

    if ("serviceWorker" in navigator) {
      window.addEventListener("load", () => {
        navigator.serviceWorker.register("./service-worker.js")
          .catch(error => console.log("Error del servicio:", error));
      });
    }

    let installPrompt;

    window.addEventListener("beforeinstallprompt", event => {
      event.preventDefault();
      installPrompt = event;
      document.getElementById("install").classList.remove("hidden");
    });

    document.getElementById("install").addEventListener("click", async () => {
      if (!installPrompt) return;
      installPrompt.prompt();
      await installPrompt.userChoice;
      installPrompt = null;
      document.getElementById("install").classList.add("hidden");
    });

    loadBooks();
  </script>
</body>
</html>
