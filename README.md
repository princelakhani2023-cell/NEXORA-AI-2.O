<!DOCTYPE html>
<html lang="en" class="dark" id="htmlRoot">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Nexora AI</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        gemini: {
                            bg: 'var(--bg-color)',
                            sidebar: 'var(--sidebar-color)',
                            card: 'var(--card-color)',
                            input: 'var(--input-color)',
                            hover: 'var(--hover-color)',
                            border: 'var(--border-color)',
                            text: 'var(--text-color)',
                            muted: 'var(--muted-color)',
                            accent: 'var(--accent-color)'
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Marked.js for Markdown parsing -->
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.js"></script>
    <!-- Highlight.js for Code Highlighting -->
    <link id="hljsTheme" rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.8.0/styles/github-dark.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.8.0/highlight.min.js"></script>
    <style>
        /* Theme Variables with Advanced Colorful Gradients */
        html.dark {
            --bg-color: #0b0c10;
            --sidebar-color: rgba(18, 19, 24, 0.85);
            --card-color: rgba(22, 23, 29, 0.9);
            --input-color: rgba(30, 32, 38, 0.85);
            --hover-color: rgba(40, 42, 50, 0.85);
            --border-color: rgba(255, 255, 255, 0.08);
            --text-color: #f1f3f4;
            --muted-color: #9aa0a6;
            --accent-color: #8ab4f8;
        }

        html:not(.dark) {
            --bg-color: #f4f6f9;
            --sidebar-color: rgba(255, 255, 255, 0.9);
            --card-color: rgba(255, 255, 255, 0.95);
            --input-color: rgba(240, 242, 245, 0.95);
            --hover-color: rgba(226, 230, 236, 0.9);
            --border-color: rgba(0, 0, 0, 0.08);
            --text-color: #202124;
            --muted-color: #5f6368;
            --accent-color: #1a73e8;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            -webkit-tap-highlight-color: transparent;
        }

        /* Colorful Ambient Background Glow Effects */
        .ambient-bg {
            position: fixed;
            width: 100vw;
            height: 100vh;
            overflow: hidden;
            z-index: 0;
            pointer-events: none;
            top: 0;
            left: 0;
        }
        .glow-blob-1 {
            position: absolute;
            top: -15%;
            left: -15%;
            width: 60vw;
            height: 60vw;
            background: radial-gradient(circle, rgba(59, 130, 246, 0.18) 0%, rgba(147, 51, 234, 0.06) 50%, transparent 70%);
            border-radius: 50%;
            filter: blur(80px);
            animation: floatBlob 10s infinite alternate ease-in-out;
        }
        .glow-blob-2 {
            position: absolute;
            bottom: -15%;
            right: -15%;
            width: 60vw;
            height: 60vw;
            background: radial-gradient(circle, rgba(236, 72, 153, 0.15) 0%, rgba(59, 130, 246, 0.06) 50%, transparent 70%);
            border-radius: 50%;
            filter: blur(80px);
            animation: floatBlob2 12s infinite alternate ease-in-out;
        }

        @keyframes floatBlob {
            0% { transform: translate(0, 0) scale(1); }
            100% { transform: translate(40px, 30px) scale(1.1); }
        }
        @keyframes floatBlob2 {
            0% { transform: translate(0, 0) scale(1); }
            100% { transform: translate(-30px, -40px) scale(1.15); }
        }

        /* Responsive Sidebar Drawer Styles for Mobile */
        @media (max-width: 768px) {
            #sidebar {
                position: fixed;
                left: 0;
                top: 0;
                height: 100%;
                z-index: 50;
                transform: translateX(-100%);
                transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
            }
            #sidebar.mobile-open {
                transform: translateX(0);
            }
            #sidebarOverlay {
                display: none;
                position: fixed;
                inset: 0;
                background: rgba(0, 0, 0, 0.5);
                backdrop-filter: blur(4px);
                z-index: 40;
            }
            #sidebarOverlay.active {
                display: block;
            }
        }

        ::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: var(--border-color);
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: var(--muted-color);
        }
        .markdown-body pre {
            background-color: var(--sidebar-color) !important;
            border: 1px solid var(--border-color);
            border-radius: 0.75rem;
            padding: 1rem;
            overflow-x: auto;
        }
        .markdown-body code {
            font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(6px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
            animation: fadeIn 0.25s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        @keyframes pulseGlow {
            0%, 100% { opacity: 0.6; }
            50% { opacity: 1; }
        }
        .animate-glow {
            animation: pulseGlow 3s infinite ease-in-out;
        }
    </style>
</head>
<body class="h-[100dvh] flex overflow-hidden font-sans relative">

    <!-- Colorful Advanced Ambient Background Blobs -->
    <div class="ambient-bg">
        <div class="glow-blob-1"></div>
        <div class="glow-blob-2"></div>
    </div>

    <!-- Mobile Sidebar Backdrop Overlay -->
    <div id="sidebarOverlay" onclick="toggleSidebar()"></div>

    <!-- SIDEBAR -->
    <aside id="sidebar" class="bg-gemini-sidebar backdrop-blur-2xl w-72 flex-shrink-0 flex flex-col z-20 border-r border-gemini-border shadow-2xl">
        <!-- Sidebar Header / New Chat Button & Search -->
        <div class="p-3.5 flex flex-col gap-2.5">
            <button onclick="createNewChat()" class="flex items-center gap-3 bg-gemini-input hover:bg-gemini-hover text-gemini-text px-4 py-3 rounded-2xl text-sm font-medium transition-all duration-200 shadow-sm w-full border border-gemini-border group">
                <i class="fa-solid fa-plus text-gemini-accent group-hover:rotate-90 transition-transform duration-300"></i>
                <span>New chat</span>
            </button>
            
            <!-- Chat Search Input Feature -->
            <div class="relative">
                <i class="fa-solid fa-search absolute left-3.5 top-1/2 -translate-y-1/2 text-gemini-muted text-xs"></i>
                <input type="text" id="chatSearchInput" oninput="filterChats(this.value)" placeholder="Search chats..." class="w-full bg-gemini-input/60 border border-gemini-border rounded-xl pl-9 pr-3 py-2 text-xs text-gemini-text placeholder-gemini-muted focus:outline-none focus:border-gemini-accent transition">
            </div>
        </div>

        <!-- Chat History List -->
        <div class="flex-1 overflow-y-auto px-3 py-1 space-y-1.5" id="chatHistoryList">
            <!-- Dynamically populated -->
        </div>

        <!-- Sidebar Footer / Theme Toggle, Dev Info & Settings -->
        <div class="p-3 border-t border-gemini-border flex flex-col gap-1 bg-gemini-sidebar/50 backdrop-blur-md">
            <!-- Theme Toggle Button -->
            <button onclick="toggleTheme()" class="flex items-center justify-between px-3 py-2 rounded-xl hover:bg-gemini-hover text-sm text-gemini-muted hover:text-gemini-text transition-all duration-200 w-full">
                <div class="flex items-center gap-3">
                    <i id="themeIcon" class="fa-solid fa-moon w-5 text-gemini-accent"></i>
                    <span id="themeText">Dark Mode</span>
                </div>
                <div class="w-8 h-4 bg-gemini-input rounded-full relative p-0.5 border border-gemini-border">
                    <div id="themeToggleDot" class="w-3 h-3 bg-gemini-accent rounded-full transition-all duration-300 transform translate-x-4"></div>
                </div>
            </button>

            <div class="flex items-center justify-between px-3 py-1.5 mt-1">
                <span class="text-xs text-gemini-muted">Dev: <strong class="text-gemini-accent font-semibold">PRINCE LAKHANI</strong></span>
                <button onclick="clearAllChats()" title="Clear All Chats" class="text-gemini-muted hover:text-red-400 p-1.5 rounded-lg hover:bg-gemini-hover transition text-xs">
                    <i class="fa-solid fa-trash"></i> Clear All
                </button>
            </div>
            <button onclick="openSettings()" class="flex items-center gap-3 px-3 py-2.5 rounded-xl hover:bg-gemini-hover text-sm text-gemini-muted hover:text-gemini-text transition-all duration-200 w-full group">
                <i class="fa-solid fa-gear w-5 group-hover:rotate-45 transition-transform duration-300"></i>
                <span>Settings</span>
            </button>
        </div>
    </aside>

    <!-- MAIN CHAT AREA -->
    <main class="flex-1 flex flex-col h-full relative z-10 min-w-0">
        <!-- Top Navbar -->
        <header class="h-14 border-b border-gemini-border/60 flex items-center justify-between px-4 bg-gemini-sidebar/60 backdrop-blur-xl z-10 flex-shrink-0">
            <div class="flex items-center gap-3 min-w-0">
                <button onclick="toggleSidebar()" class="text-gemini-muted hover:text-gemini-text p-2 rounded-xl hover:bg-gemini-hover transition-all flex-shrink-0">
                    <i class="fa-solid fa-bars text-lg"></i>
                </button>
                <div class="flex items-center gap-2.5 min-w-0">
                    <span class="font-bold text-base md:text-lg bg-gradient-to-r from-blue-400 via-indigo-400 to-purple-400 bg-clip-text text-transparent tracking-wide flex-shrink-0">Nexora AI</span>
                    <span id="currentModelDisplay" class="text-[11px] md:text-xs px-2 py-0.5 rounded-lg bg-gemini-input border border-gemini-border text-gemini-muted font-mono truncate max-w-[140px] md:max-w-xs">google/gemini-2.0-flash-exp:free</span>
                </div>
            </div>
            <div class="flex items-center gap-2 flex-shrink-0">
                <button onclick="openSettings()" class="text-gemini-muted hover:text-gemini-text p-2 rounded-xl hover:bg-gemini-hover transition-all" title="Settings">
                    <i class="fa-solid fa-sliders text-sm"></i>
                </button>
            </div>
        </header>

        <!-- Chat Content Scroll Area -->
        <div id="chatScrollArea" class="flex-1 overflow-y-auto px-4 py-6 flex flex-col items-center">
            <!-- Welcome Container / Message List Container -->
            <div id="chatContainer" class="w-full max-w-3xl flex flex-col space-y-6 pb-4">
                <!-- Populated dynamically via JS -->
            </div>
        </div>

        <!-- Input Bar Section -->
        <div class="p-3 md:p-4 bg-gradient-to-t from-gemini-bg via-gemini-bg/90 to-transparent flex flex-col items-center z-10 flex-shrink-0">
            <div class="w-full max-w-3xl relative">
                <div class="bg-gemini-card backdrop-blur-xl border border-gemini-border rounded-3xl p-2.5 flex flex-col shadow-2xl focus-within:border-gemini-accent focus-within:ring-1 focus-within:ring-gemini-accent/30 transition-all duration-300">
                    <textarea id="userInput" rows="1" placeholder="Ask Nexora anything..." class="w-full bg-transparent text-gemini-text placeholder-gemini-muted px-3 py-1.5 text-sm md:text-base focus:outline-none resize-none max-h-36" oninput="autoResize(this)" onkeydown="handleKeyDown(event)"></textarea>
                    
                    <div class="flex items-center justify-between px-2 pt-1">
                        <div class="flex items-center gap-1 text-gemini-muted text-xs">
                            <span id="tokenStatus" class="flex items-center gap-1.5">
                                <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                                <span class="hidden sm:inline">Nexora Engine Ready</span>
                                <span class="sm:hidden">Ready</span>
                            </span>
                        </div>
                        <div class="flex items-center gap-2">
                            <button id="sendBtn" onclick="sendMessage()" class="bg-gradient-to-r from-blue-500 to-purple-500 text-white rounded-full w-9 h-9 flex items-center justify-center hover:opacity-95 hover:scale-105 active:scale-95 transition-all duration-200 shadow-lg disabled:opacity-40 disabled:scale-100 disabled:cursor-not-allowed">
                                <i class="fa-solid fa-arrow-up text-sm"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="text-center text-[11px] md:text-xs text-gemini-muted/70 mt-2">
                Nexora AI is created by <strong class="text-gemini-accent font-medium">PRINCE LAKHANI</strong>.
            </div>
        </div>
    </main>

    <!-- SETTINGS MODAL -->
    <div id="settingsModal" class="fixed inset-0 bg-black/60 backdrop-blur-md z-50 hidden flex items-center justify-center p-4 transition-all duration-300">
        <div class="bg-gemini-card backdrop-blur-xl border border-gemini-border w-full max-w-md rounded-3xl shadow-2xl overflow-hidden flex flex-col animate-fade-in">
            <div class="px-6 py-5 border-b border-gemini-border flex items-center justify-between">
                <h3 class="text-lg font-semibold text-gemini-text">API Settings</h3>
                <button onclick="closeSettings()" class="text-gemini-muted hover:text-gemini-text w-8 h-8 rounded-xl hover:bg-gemini-hover flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <div class="p-6 space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gemini-muted mb-1.5">OpenRouter API Key</label>
                    <input type="password" id="apiKeyInput" placeholder="sk-or-v1-..." class="w-full bg-gemini-input border border-gemini-border rounded-2xl px-4 py-3 text-gemini-text focus:outline-none focus:border-gemini-accent text-sm transition">
                    <p class="text-xs text-gemini-muted mt-1.5">Get your key from <a href="https://openrouter.ai/keys" target="_blank" class="text-gemini-accent underline hover:opacity-80">openrouter.ai/keys</a></p>
                </div>
                <div>
                    <label class="block text-sm font-medium text-gemini-muted mb-1.5">Model Name</label>
                    <input type="text" id="modelInput" placeholder="google/gemini-2.0-flash-exp:free" class="w-full bg-gemini-input border border-gemini-border rounded-2xl px-4 py-3 text-gemini-text focus:outline-none focus:border-gemini-accent text-sm transition">
                    <p class="text-xs text-gemini-muted mt-1.5">E.g., <code>google/gemini-2.0-flash-exp:free</code></p>
                </div>
            </div>
            <div class="px-6 py-4 border-t border-gemini-border flex justify-end gap-3 bg-gemini-sidebar/50">
                <button onclick="closeSettings()" class="px-5 py-2.5 rounded-xl text-sm font-medium hover:bg-gemini-hover text-gemini-muted hover:text-gemini-text transition">Cancel</button>
                <button onclick="saveSettings()" class="px-5 py-2.5 rounded-xl text-sm font-medium bg-gradient-to-r from-blue-500 to-purple-500 text-white hover:opacity-95 shadow-md transition">Save Changes</button>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC BLOCK -->
    <script>
        let state = {
            apiKey: localStorage.getItem('nexora_api_key') || '',
            modelName: localStorage.getItem('nexora_model_name') || 'google/gemini-2.0-flash-exp:free',
            currentChatId: null,
            chats: JSON.parse(localStorage.getItem('nexora_chats') || '[]'),
            isGenerating: false,
            searchQuery: '',
            isDarkMode: localStorage.getItem('nexora_theme') !== 'light'
        };

        document.addEventListener('DOMContentLoaded', () => {
            applyTheme(state.isDarkMode);

            marked.setOptions({
                highlight: function(code, lang) {
                    if (lang && hljs.getLanguage(lang)) {
                        return hljs.highlight(code, { language: lang }).value;
                    }
                    return hljs.highlightAuto(code).value;
                },
                breaks: true,
                gfm: true
            });

            updateModelDisplay();
            renderSidebar();

            if (state.chats.length === 0) {
                createNewChat();
            } else {
                loadChat(state.chats[0].id);
            }
        });

        function toggleTheme() {
            state.isDarkMode = !state.isDarkMode;
            localStorage.setItem('nexora_theme', state.isDarkMode ? 'dark' : 'light');
            applyTheme(state.isDarkMode);
        }

        function applyTheme(isDark) {
            const htmlRoot = document.getElementById('htmlRoot');
            const themeIcon = document.getElementById('themeIcon');
            const themeText = document.getElementById('themeText');
            const themeToggleDot = document.getElementById('themeToggleDot');
            const hljsTheme = document.getElementById('hljsTheme');

            if (isDark) {
                htmlRoot.classList.add('dark');
                themeIcon.className = 'fa-solid fa-moon w-5 text-gemini-accent';
                themeText.innerText = 'Dark Mode';
                themeToggleDot.style.transform = 'translateX(1rem)';
                hljsTheme.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.8.0/styles/github-dark.min.css';
            } else {
                htmlRoot.classList.remove('dark');
                themeIcon.className = 'fa-solid fa-sun w-5 text-amber-500';
                themeText.innerText = 'Light Mode';
                themeToggleDot.style.transform = 'translateX(0rem)';
                hljsTheme.href = 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.8.0/styles/github.min.css';
            }
        }

        function autoResize(textarea) {
            textarea.style.height = 'auto';
            textarea.style.height = Math.min(textarea.scrollHeight, 140) + 'px';
        }

        function handleKeyDown(event) {
            if (event.key === 'Enter' && !event.shiftKey) {
                event.preventDefault();
                sendMessage();
            }
        }

        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const overlay = document.getElementById('sidebarOverlay');
            sidebar.classList.toggle('mobile-open');
            overlay.classList.toggle('active');
        }

        function openSettings() {
            document.getElementById('apiKeyInput').value = state.apiKey;
            document.getElementById('modelInput').value = state.modelName;
            document.getElementById('settingsModal').classList.remove('hidden');
        }

        function closeSettings() {
            document.getElementById('settingsModal').classList.add('hidden');
        }

        function saveSettings() {
            state.apiKey = document.getElementById('apiKeyInput').value.trim();
            state.modelName = document.getElementById('modelInput').value.trim() || 'google/gemini-2.0-flash-exp:free';
            
            localStorage.setItem('nexora_api_key', state.apiKey);
            localStorage.setItem('nexora_model_name', state.modelName);

            updateModelDisplay();
            closeSettings();
        }

        function updateModelDisplay() {
            document.getElementById('currentModelDisplay').innerText = state.modelName;
        }

        function createNewChat() {
            const newChat = {
                id: 'chat_' + Date.now(),
                title: 'New Conversation',
                messages: []
            };
            state.chats.unshift(newChat);
            saveChatsToStorage();
            renderSidebar();
            loadChat(newChat.id);
            if (window.innerWidth < 768) {
                const sidebar = document.getElementById('sidebar');
                if (sidebar.classList.contains('mobile-open')) toggleSidebar();
            }
        }

        function loadChat(chatId) {
            state.currentChatId = chatId;
            renderSidebar();
            renderActiveChat();
            if (window.innerWidth < 768) {
                const sidebar = document.getElementById('sidebar');
                if (sidebar.classList.contains('mobile-open')) toggleSidebar();
            }
        }

        function deleteChat(chatId, event) {
            event.stopPropagation();
            state.chats = state.chats.filter(c => c.id !== chatId);
            saveChatsToStorage();
            renderSidebar();
            if (state.currentChatId === chatId) {
                if (state.chats.length > 0) {
                    loadChat(state.chats[0].id);
                } else {
                    createNewChat();
                }
            }
        }

        function clearAllChats() {
            if (confirm("Are you sure you want to clear all chat history?")) {
                state.chats = [];
                saveChatsToStorage();
                createNewChat();
            }
        }

        function filterChats(query) {
            state.searchQuery = query.toLowerCase();
            renderSidebar();
        }

        function saveChatsToStorage() {
            localStorage.setItem('nexora_chats', JSON.stringify(state.chats));
        }

        function renderSidebar() {
            const listEl = document.getElementById('chatHistoryList');
            listEl.innerHTML = '';

            const filteredChats = state.chats.filter(chat => 
                chat.title.toLowerCase().includes(state.searchQuery)
            );

            if (filteredChats.length === 0) {
                listEl.innerHTML = `<div class="px-3 py-4 text-xs text-center text-gemini-muted">No chats found</div>`;
                return;
            }

            filteredChats.forEach(chat => {
                const isActive = chat.id === state.currentChatId;
                const item = document.createElement('div');
                item.className = `group flex items-center justify-between px-3.5 py-2.5 rounded-xl text-sm cursor-pointer transition-all duration-200 ${isActive ? 'bg-gemini-input text-gemini-text font-medium shadow-sm border border-gemini-border' : 'text-gemini-muted hover:bg-gemini-hover hover:text-gemini-text'}`;
                item.onclick = () => loadChat(chat.id);
                
                item.innerHTML = `
                    <div class="flex items-center gap-3 truncate">
                        <i class="fa-regular fa-message text-xs w-4"></i>
                        <span class="truncate">${escapeHtml(chat.title)}</span>
                    </div>
                    <button onclick="deleteChat('${chat.id}', event)" class="opacity-0 group-hover:opacity-100 text-gemini-muted hover:text-red-400 p-1.5 rounded-lg hover:bg-gemini-card transition">
                        <i class="fa-solid fa-trash-can text-xs"></i>
                    </button>
                `;
                listEl.appendChild(item);
            });
        }

        function renderActiveChat() {
            const container = document.getElementById('chatContainer');
            container.innerHTML = '';

            const currentChat = state.chats.find(c => c.id === state.currentChatId);
            if (!currentChat) return;

            if (currentChat.messages.length === 0) {
                container.innerHTML = `
                    <div class="flex flex-col items-center justify-center my-auto py-16 text-center animate-fade-in px-4">
                        <div class="w-16 h-16 md:w-20 md:h-20 rounded-3xl bg-gradient-to-tr from-blue-500 via-indigo-500 to-purple-500 flex items-center justify-center mb-5 shadow-2xl animate-glow">
                            <i class="fa-solid fa-sparkles text-2xl md:text-3xl text-white"></i>
                        </div>
                        <h1 class="text-2xl md:text-3xl font-bold text-gemini-text mb-2 tracking-tight">Welcome to Nexora AI</h1>
                        <p class="text-gemini-muted text-sm md:text-base">Developed by <strong class="text-gemini-accent font-semibold">Prince Lakhani</strong>. How can I help you today?</p>
                    </div>
                `;
                return;
            }

            currentChat.messages.forEach(msg => {
                appendMessageNode(msg.role, msg.content);
            });

            scrollToBottom();
        }

        function appendMessageNode(role, content) {
            const container = document.getElementById('chatContainer');
            const isUser = role === 'user';

            const wrapper = document.createElement('div');
            wrapper.className = `flex gap-3 md:gap-4 w-full animate-fade-in ${isUser ? 'justify-end' : 'justify-start'}`;

            if (!isUser) {
                const avatar = document.createElement('div');
                avatar.className = 'w-8 h-8 md:w-9 md:h-9 rounded-2xl bg-gradient-to-tr from-blue-500 to-purple-600 flex items-center justify-center flex-shrink-0 mt-1 shadow-lg';
                avatar.innerHTML = '<i class="fa-solid fa-sparkles text-xs text-white"></i>';
                wrapper.appendChild(avatar);
            }

            const bubble = document.createElement('div');
            bubble.className = `max-w-[88%] md:max-w-[85%] rounded-3xl px-4 md:px-5 py-3 md:py-4 text-sm leading-relaxed ${isUser ? 'bg-gemini-input text-gemini-text border border-gemini-border rounded-br-lg shadow-sm' : 'text-gemini-text w-full'}`;

            if (isUser) {
                bubble.innerText = content;
            } else {
                bubble.innerHTML = `<div class="markdown-body">${marked.parse(content || '')}</div>`;
                bubble.querySelectorAll('pre code').forEach((block) => {
                    hljs.highlightElement(block);
                });
            }

            wrapper.appendChild(bubble);
            container.appendChild(wrapper);
        }

        async function sendMessage() {
            if (state.isGenerating) return;

            const inputEl = document.getElementById('userInput');
            const promptText = inputEl.value.trim();
            if (!promptText) return;

            if (!state.apiKey) {
                alert('Please configure your OpenRouter API Key in the Settings menu first.');
                openSettings();
                return;
            }

            inputEl.value = '';
            inputEl.style.height = 'auto';

            const currentChat = state.chats.find(c => c.id === state.currentChatId);
            if (!currentChat) return;

            if (currentChat.messages.length === 0) {
                currentChat.title = promptText.length > 25 ? promptText.substring(0, 25) + '...' : promptText;
            }

            currentChat.messages.push({ role: 'user', content: promptText });
            saveChatsToStorage();
            renderSidebar();
            renderActiveChat();

            state.isGenerating = true;
            document.getElementById('sendBtn').disabled = true;

            currentChat.messages.push({ role: 'assistant', content: '' });
            renderActiveChat();

            try {
                const response = await fetch("https://openrouter.ai/api/v1/chat/completions", {
                    method: "POST",
                    headers: {
                        "Authorization": `Bearer ${state.apiKey}`,
                        "HTTP-Referer": window.location.href,
                        "X-Title": "Nexora AI",
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify({
                        model: state.modelName,
                        messages: currentChat.messages.slice(0, -1).map(m => ({ role: m.role, content: m.content })),
                        stream: true
                    })
                });

                if (!response.ok) {
                    const errData = await response.json().catch(() => ({}));
                    throw new Error(errData.error?.message || `API Error Status: ${response.status}`);
                }

                const reader = response.body.getReader();
                const decoder = new TextDecoder("utf-8");
                let accumulatedText = "";

                while (true) {
                    const { done, value } = await reader.read();
                    if (done) break;

                    const chunk = decoder.decode(value, { stream: true });
                    const lines = chunk.split("\n");

                    for (const line of lines) {
                        const trimmed = line.trim();
                        if (trimmed.startsWith("data:")) {
                            const jsonStr = trimmed.substring(5).trim();
                            if (jsonStr === "[DONE]") break;
                            try {
                                const parsed = JSON.parse(jsonStr);
                                const contentChunk = parsed.choices[0]?.delta?.content || "";
                                if (contentChunk) {
                                    accumulatedText += contentChunk;
                                    currentChat.messages[currentChat.messages.length - 1].content = accumulatedText;
                                    updateLastMessageContent(accumulatedText);
                                }
                            } catch (e) {}
                        }
                    }
                }

                saveChatsToStorage();

            } catch (error) {
                console.error(error);
                const errorMsg = `⚠️ **Connection Error:**\n> ${error.message}\n\n*Please check if your OpenRouter API Key and Model Name are valid in Settings.*`;
                currentChat.messages[currentChat.messages.length - 1].content = errorMsg;
                updateLastMessageContent(errorMsg);
                saveChatsToStorage();
            } finally {
                state.isGenerating = false;
                document.getElementById('sendBtn').disabled = false;
                renderActiveChat();
            }
        }

        function updateLastMessageContent(text) {
            const container = document.getElementById('chatContainer');
            const lastAssistantBubble = container.lastElementChild?.querySelector('.markdown-body');
            if (lastAssistantBubble) {
                lastAssistantBubble.innerHTML = marked.parse(text || '');
                lastAssistantBubble.querySelectorAll('pre code').forEach((block) => {
                    hljs.highlightElement(block);
                });
                scrollToBottom();
            }
        }

        function scrollToBottom() {
            const scrollArea = document.getElementById('chatScrollArea');
            scrollArea.scrollTop = scrollArea.scrollHeight;
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>
