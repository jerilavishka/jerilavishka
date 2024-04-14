from flask import Flask, render_template

app = Flask(__animeplayer__)

# Sample anime data with servers
anime_list = [
    {
        "title": "Naruto",
        "description": "A story about a young ninja named Naruto who seeks recognition from his peers.",
        "servers": [
            {"name": "Server 1", "link": "https://www.example.com/naruto_episode_1"},
            {"name": "Server 2", "link": "https://www.example.com/naruto_episode_1"}
        ]
    },
    {
        "title": "Attack on Titan",
        "description": "Humans face off against giant humanoid creatures known as Titans.",
        "servers": [
            {"name": "Server 1", "link": "https://www.example.com/aot_episode_1"},
            {"name": "Server 2", "link": "https://www.example.com/aot_episode_1"}
        ]
    },
    {
        "title": "My Hero Academia",
        "description": "Follows the story of Izuku Midoriya, a boy born without superpowers in a world where they are the norm.",
        "servers": [
            {"name": "Server 1", "link": "https://www.example.com/mha_episode_1"},
            {"name": "Server 2", "link": "https://www.example.com/mha_episode_1"}
        ]
    },
]

@app.route('/')
def index():
    return render_template('index.html', anime_list=anime_list)

@app.route('/anime/<int:index>')
def anime(index):
    anime = anime_list[index]
    return render_template('anime.html', anime=anime)

if __name__ == '__main__':
    app.run(debug=True)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AnimePlayer - {{ anime.title }}</title>
</head>
<body>
    <h1>{{ anime.title }}</h1>
    <p>{{ anime.description }}</p>
    <h2>Streaming Links</h2>
    <ul>
        {% for server in anime.servers %}
            <li><a href="{{ server.link }}">{{ server.name }}</a></li>
        {% endfor %}
    </ul>
    <a href="/">Back to Home</a>
</body>
</html>

