# webpanel
panel discord
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Panel de gestion du bot Discord</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body {
            background-color: #f8f9fa;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }
        .navbar {
            background-color: #007BFF;
            color: white;
            font-size: 18px;
            padding: 12px;
            position: fixed;
            width: calc(100% - 200px);
            top: 0;
            left: 200px;
            z-index: 1000;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .navbar h1 {
            margin: 0;
            font-size: 24px;
        }
        .logout-button {
            margin-right: 20px;
        }
        .sidebar {
            background-color: #ffffff;
            color: #333333;
            font-size: 18px;
            padding: 12px;
            position: fixed;
            width: 200px;
            height: 100vh;
            top: 0;
            left: 0;
            border-right: 1px solid #ddd;
            z-index: 999;
            display: flex;
            flex-direction: column;
            align-items: center;
            box-shadow: 2px 0 5px rgba(0,0,0,0.1);
        }
        .sidebar h2 {
            margin-bottom: 20px;
        }
        .container {
            margin-left: 200px;
            margin-top: 60px;
            padding: 20px;
        }
        .nav-pills {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .nav-pills .nav-link {
            border-radius: 0;
            margin-bottom: 1px;
        }
        .nav-item {
            width: 100%;
        }
        .form-section {
            display: none;
            width: 100%;
        }
        footer {
            background-color: #ffffff;
            color: #333333;
            text-align: center;
            padding: 10px 0;
            font-size: 14px;
            position: fixed;
            width: calc(100% - 200px);
            bottom: 0;
            left: 200px;
        }
        .page-title {
            font-size: 2rem;
            margin-bottom: 20px;
            text-align: center;
        }
        .embed-container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }
        .embed-section {
            background-color: #f9f9f9;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            flex: 1;
            min-width: 300px;
        }
        .left-embed {
            max-width: 400px;
            margin-right: auto;
        }
        .embed-section h4 {
            margin-top: 0;
        }
        .embed-section .form-group {
            margin-bottom: 15px;
        }
        .embed-section .btn {
            width: 100%;
        }
        /* Console de logs */
        .console-logs {
            background-color: #000;
            color: #0f0;
            padding: 10px;
            height: 300px;
            overflow-y: scroll;
            font-family: monospace;
            white-space: pre-wrap;
            border: 1px solid #ddd;
        }
        @media (max-width: 768px) {
            .navbar, footer {
                width: 100%;
                left: 0;
            }
            .container {
                margin-left: 0;
            }
        }
    </style>
</head>
<body>
    <div class="navbar">
        <h1>arcos web api</h1>
        <button class="btn btn-danger logout-button">Déconnexion</button>
    </div>

    <div class="sidebar">
        <h2>Menu</h2>
        <div class="nav flex-column nav-pills" id="v-pills-tab" role="tablist" aria-orientation="vertical">
            <a class="nav-link active" id="home-tab" data-bs-toggle="pill" data-bs-target="#home" role="tab" aria-controls="home" aria-selected="true">Accueil</a>
            <a class="nav-link" id="sendMessage-tab" data-bs-toggle="pill" data-bs-target="#sendMessage" role="tab" aria-controls="sendMessage" aria-selected="false">Envoyer un Message</a>
            <a class="nav-link" id="sendEmbed-tab" data-bs-toggle="pill" data-bs-target="#sendEmbed" role="tab" aria-controls="sendEmbed" aria-selected="false">Envoyer un Embed</a>
            <a class="nav-link" id="clearMessages-tab" data-bs-toggle="pill" data-bs-target="#clearMessages" role="tab" aria-controls="clearMessages" aria-selected="false">Effacer des Messages</a>
            <a class="nav-link" id="banUser-tab" data-bs-toggle="pill" data-bs-target="#banUser" role="tab" aria-controls="banUser" aria-selected="false">Bannir un Utilisateur</a>
            <a class="nav-link" id="logs-tab" data-bs-toggle="pill" data-bs-target="#logs" role="tab" aria-controls="logs" aria-selected="false">Logs</a>
        </div>
    </div>

    <div class="container">
        <div class="tab-content" id="myTabContent">
            <!-- Page d'accueil -->
            <div class="tab-pane fade show active" id="home" role="tabpanel" aria-labelledby="home-tab">
                <h2 class="page-title">Bienvenue sur arcos développement !</h2>
                <p>Nous sommes ravis de vous accueillir sur notre plateforme, où la création, l'hébergement, et la gestion de vos bots deviennent un jeu d'enfant.</p>
            </div>

            <!-- Page pour Envoyer un Message -->
            <div class="tab-pane fade" id="sendMessage" role="tabpanel" aria-labelledby="sendMessage-tab">
                <h2 class="page-title">Envoyer un Message</h2>
                <div class="embed-container">
                    <div class="embed-section left-embed" id="sendMessageEmbed">
                        <h4>Envoyer un Message</h4>
                        <form id="sendMessageForm">
                            <div class="form-group">
                                <label for="channelIdMessage">ID du canal</label>
                                <input type="text" class="form-control" id="channelIdMessage" name="channelId" placeholder="Saisissez l'ID du canal" required>
                            </div>
                            <div class="form-group">
                                <label for="sendMessageContent">Message</label>
                                <input type="text" class="form-control" id="sendMessageContent" name="message" placeholder="Saisissez votre message" required>
                            </div>
                            <div class="form-group">
                                <label for="usernameMessage">Nom d'utilisateur</label>
                                <input type="text" class="form-control" id="usernameMessage" name="username" placeholder="Saisissez votre nom d'utilisateur" required>
                            </div>
                            <button type="submit" class="btn btn-primary">Envoyer le message</button>
                        </form>
                    </div>
                </div>
            </div>

            <!-- Page pour Envoyer un Embed -->
            <div class="tab-pane fade" id="sendEmbed" role="tabpanel" aria-labelledby="sendEmbed-tab">
                <h2 class="page-title">Envoyer un Embed</h2>
                <div class="embed-container">
                    <div class="embed-section left-embed" id="sendEmbedEmbed">
                        <h4>Envoyer un Embed</h4>
                        <form id="sendEmbedForm">
                            <div class="form-group">
                                <label for="channelIdEmbed">ID du canal</label>
                                <input type="text" class="form-control" id="channelIdEmbed" name="channelId" placeholder="Saisissez l'ID du canal" required>
                            </div>
                            <div class="form-group">
                                <label for="embedTitle">Titre de l'embed</label>
                                <input type="text" class="form-control" id="embedTitle" name="title" placeholder="Saisissez le titre de l'embed" required>
                            </div>
                            <div class="form-group">
                                <label for="embedDescription">Description de l'embed</label>
                                <textarea class="form-control" id="embedDescription" name="description" placeholder="Saisissez la description de l'embed" required></textarea>
                            </div>
                            <div class="form-group">
                                <label for="embedColor">Couleur de l'embed</label>
                                <input type="color" class="form-control form-control-color" id="embedColor" name="color" value="#000000" required>
                            </div>
                            <button type="submit" class="btn btn-primary">Envoyer l'embed</button>
                        </form>
                    </div>
                </div>
            </div>

            <!-- Page pour Effacer des Messages -->
            <div class="tab-pane fade" id="clearMessages" role="tabpanel" aria-labelledby="clearMessages-tab">
                <h2 class="page-title">Effacer des Messages</h2>
                <div class="embed-container">
                    <div class="embed-section left-embed" id="clearMessagesEmbed">
                        <h4>Effacer des Messages</h4>
                        <form id="clearMessagesForm">
                            <div class="form-group">
                                <label for="channelIdClear">ID du canal</label>
                                <input type="text" class="form-control" id="channelIdClear" name="channelId" placeholder="Saisissez l'ID du canal" required>
                            </div>
                            <div class="form-group">
                                <label for="messageCount">Nombre de messages à effacer</label>
                                <input type="number" class="form-control" id="messageCount" name="count" placeholder="Nombre de messages" required>
                            </div>
                            <button type="submit" class="btn btn-danger">Effacer les messages</button>
                        </form>
                    </div>
                </div>
            </div>

            <!-- Page pour Bannir un Utilisateur -->
            <div class="tab-pane fade" id="banUser" role="tabpanel" aria-labelledby="banUser-tab">
                <h2 class="page-title">Bannir un Utilisateur</h2>
                <div class="embed-container">
                    <div class="embed-section left-embed" id="banUserEmbed">
                        <h4>Bannir un Utilisateur</h4>
                        <form id="banUserForm">
                            <div class="form-group">
                                <label for="userIdBan">ID de l'utilisateur</label>
                                <input type="text" class="form-control" id="userIdBan" name="userId" placeholder="Saisissez l'ID de l'utilisateur" required>
                            </div>
                            <div class="form-group">
                                <label for="banReason">Raison du bannissement</label>
                                <textarea class="form-control" id="banReason" name="reason" placeholder="Saisissez la raison du bannissement" required></textarea>
                            </div>
                            <div class="form-group">
                                <label for="banDuration">Durée du bannissement (en jours)</label>
                                <input type="number" class="form-control" id="banDuration" name="duration" placeholder="Durée du bannissement" required>
                            </div>
                            <button type="submit" class="btn btn-danger">Bannir l'utilisateur</button>
                        </form>
                    </div>
                </div>
            </div>

            <!-- Page des Logs -->
            <div class="tab-pane fade" id="logs" role="tabpanel" aria-labelledby="logs-tab">
                <h2 class="page-title">Logs</h2>
                <div class="console-logs" id="consoleLogs">
                    <!-- Les logs seront affichés ici -->
                </div>
            </div>
        </div>
    </div>

    <footer>
        &copy; 2024 Panel de gestion du bot Discord. Tous droits réservés.
    </footer>

    <!-- Ajout de la connexion WebSocket pour les logs -->
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Gestion des onglets
            const tabs = document.querySelectorAll('.nav-link');
            const contents = document.querySelectorAll('.tab-pane');

            tabs.forEach(tab => {
                tab.addEventListener('click', function() {
                    tabs.forEach(t => t.classList.remove('active'));
                    contents.forEach(content => content.classList.remove('show', 'active'));

                    this.classList.add('active');
                    const target = document.querySelector(this.getAttribute('data-bs-target'));
                    target.classList.add('show', 'active');
                });
            });

            // Simuler l'ajout de logs dans la console
            const consoleLogs = document.getElementById('consoleLogs');
            function addLog(message) {
                const logEntry = document.createElement('div');
                logEntry.textContent = message;
                consoleLogs.appendChild(logEntry);
                consoleLogs.scrollTop = consoleLogs.scrollHeight; // Défile automatiquement vers le bas
            }

            // Ajouter des logs toutes les 2 secondes (simulation)
            setInterval(() => {
                const time = new Date().toLocaleTimeString();
                addLog(`[${time}] Log message simulé ajouté.`);
            }, 2000);
        });
    </script>
</body>
</html>
