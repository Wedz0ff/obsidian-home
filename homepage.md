---
cssclass: document--no-title
banner: "https://i.imgur.com/0MIMCQx.png"
banner_y: 0.268
---

# おかえりなさい (Okaerinasai), senpai!

```dataviewjs
const categories = ['happy', 'wave', 'thumbsup', 'dance'];
const currentCategory = categories[Math.floor(Math.random() * categories.length)];
const gifApiUrl = `https://nekos.best/api/v2/${currentCategory}`;
const fallbackGif = 'https://i.imgur.com/rT548IP.gif';
const loadingGif = 'https://i.imgur.com/uu0WSB9.gif'

const container = dv.container;
container.innerHTML = '';

const paragraph = container.createEl('p', {
    attr: {
        align: 'center'
    }
});
const imgElement = paragraph.createEl('img', {
    attr: {
        src: loadingGif,
        alt: 'Loading GIF...',
        width: '400'
    }
});

(async () => {
    try {
        const response = await fetch(gifApiUrl);

        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const data = await response.json();
        const gif = data?.results?.[0];

        if (!gif?.url) {
            throw new Error('No valid GIF URL found in the API response.');
        }

        imgElement.src = gif.url;
        imgElement.alt = gif.anime_name || 'Anime GIF';

    } catch (error) {
        console.error('Failed to fetch GIF:', error);
        imgElement.src = fallbackGif;
        imgElement.alt = `Fallback GIF - Error: ${error.message}`;
    }
})();
```
---

```dataviewjs
const currentCity = 'balneário camboriú';
const apiUrl = `https://api.wedzy.net/weather?city=${encodeURIComponent(currentCity)}`;
const container = dv.container;
container.innerHTML = '';

const iconMap = {
    '01d': '☀️',
    '01n': '🌙',
    '02d': '⛅',
    '02n': '☁️',
    '03d': '☁️',
    '03n': '☁️',
    '04d': '🌥️',
    '04n': '🌥️',
    '09d': '🌧️',
    '09n': '🌧️',
    '10d': '🌦️',
    '10n': '🌧️',
    '11d': '⛈️',
    '11n': '⛈️',
    '13d': '❄️',
    '13n': '❄️',
    '50d': '🌫️',
    '50n': '🌫️'
};

(async () => {
    try {
        const response = await fetch(apiUrl);
        if (!response.ok) throw new Error(`HTTP error! Status: ${response.status}`);

        const data = await response.json();
        const weather = data.weather[0];
        const iconEmoji = iconMap[weather.icon] || '🌈';

        const layout = container.createEl('div', {
            attr: {
                style: `
                    display: flex;
                    justify-content: space-between;
                    gap: 1.5em;
                    padding: 1.5em;                   
                `
            }
        });

        const card = layout.createEl('div', {
            cls: 'weather-card',
            attr: {
                style: `
                    flex: 1;
                `
            }
        });

        card.createEl('p', {
            text: `${iconEmoji} Weather in ${data.name}`,
            attr: {
                style: 'font-weight: bold; margin-bottom: 0.5em; font-size: 1.2em;'
            }
        });

        card.createEl('p', {
            text: `🌡️ Temp: ${data.main.temp.toFixed(1)}°C (feels like ${data.main.feels_like.toFixed(1)}°C)`,
            attr: {
                style: 'margin: 0.3em 0;'
            }
        });

        card.createEl('p', {
            text: `📈 Min: ${data.main.temp_min.toFixed(1)}°C - Max: ${data.main.temp_max.toFixed(1)}°C`,
            attr: {
                style: 'margin: 0.3em 0;'
            }
        });

        card.createEl('p', {
            text: `☁️ Condition: ${weather.description.charAt(0).toUpperCase() + weather.description.slice(1)}`,
            attr: {
                style: 'margin: 0.3em 0;'
            }
        });

        layout.createEl('img', {
            attr: {
                src: 'https://i.imgur.com/q1XsLaG.png',
                width: '172',
                alt: 'mikku',
            }
        });

    } catch (error) {
        container.createEl('p', {
            text: `❌ Could not load weather: ${error.message}`
        });
    }
})();
```
---

<div class="dashboard-section info-box anime-theme-box">

## 🧠 今日の言葉 (Word of the Day)

```dataviewjs
const levels = ['A1', 'A2', 'B1', 'B2']; // can add up to C2
const selectedLevel = levels[Math.floor(Math.random() * levels.length)];
const apiUrl = `https://api.wedzy.net/random-de-word?level=${selectedLevel}`;
const container = dv.container;
container.innerHTML = '';

const card = container.createEl('div', {
    attr: {
        style: `
      margin-left: 1.5em;
    `
    }
});

(async () => {
    try {
        const response = await fetch(apiUrl);
        if (!response.ok) throw new Error(`HTTP error! Status: ${response.status}`);

        const data = await response.json();

        const layout = container.createEl('div', {
            attr: {
                style: `
                
                    margin-left: 1.5em;                   
        
                `
            }
        });

        const card = layout.createEl('div', {
            cls: 'deutsch-card',
        });

        card.createEl('p', {
            text: `Deutsch:`,
            attr: {
                style: 'font-weight: bold; margin-bottom: 0.5em; font-size: 1.2em;'
            }
        });

        card.createEl('p', {
            text: `🔤 Word: ${data.lemma} (${data.type})`,
            attr: {
                style: 'margin: 0.4em 0; font-weight: bold;'
            }
        });

        card.createEl('p', {
            text: `📚 Level: ${data.level}`,
            attr: {
                style: 'margin: 0.4em 0;'
            }
        });

        card.createEl('p', {
            text: `🌍 English: ${data.translations.en.join(', ')}`,
            attr: {
                style: 'margin: 0.4em 0;'
            }
        });

    } catch (error) {
        container.createEl('p', {
            text: `❌ couldn't not load Deutsch word: ${error.message}`
        });
    }
})();
```

```dataviewjs
const levels = [5, 4, 3]; // can add up to 5 ;p
const selectedLevel = levels[Math.floor(Math.random() * levels.length)];
const apiUrl = `https://api.wedzy.net/random-jp-word?level=${selectedLevel}`;
const container = dv.container;
container.innerHTML = '';

const card = container.createEl('div', {
    attr: {
        style: `
      margin-left: 1.5em;
    `
    }
});

(async () => {
    try {
        const response = await fetch(apiUrl);
        if (!response.ok) throw new Error(`HTTP error! Status: ${response.status}`);

        const data = await response.json();

        const layout = container.createEl('div', {
            attr: {
                style: `
                
                    margin-left: 1.5em;                   
                `
            }
        });

        const card = layout.createEl('div', {
            cls: 'japanese-card',
        });

        card.createEl('p', {
            text: `日本語:`,
            attr: {
                style: 'font-weight: bold; margin-bottom: 0.5em; font-size: 1.2em;'
            }
        });

        card.createEl('p', {
            text: `🔤 Word: ${data.word} (${data.romaji})`,
            attr: {
                style: 'margin: 0.4em 0; font-weight: bold;'
            }
        });

        if (data.furigana && data.furigana.length > 0) {
            card.createEl('p', {
                text: `📚 Furigana: ${data.furigana}`,
                attr: {
                    style: 'margin: 0.4em 0;'
                }
            })
        }
       
        card.createEl('p', {
            text: `📚 Level: N${data.level}`,
            attr: {
                style: 'margin: 0.4em 0;'
            }
        });

        card.createEl('p', {
            text: `🌍 English: ${data.meaning}`,
            attr: {
                style: 'margin: 0.4em 0;'
            }
        });

    } catch (error) {
        container.createEl('p', {
            text: `❌ Couldn't load japanese word: ${error.message}`
        });
    }
})();
```
</div>

---

<div class="dashboard-section info-box anime-theme-box">

## ✨ 今日の豆知識 (Trivia/Curiosity)

```dataviewjs
const apiUrl = `https://kawaii-api.wedzy.net/random-curiosity`;
const container = dv.container;
container.innerHTML = '';

const card = container.createEl('div', {
    attr: {
        style: `
      margin-left: 1.5em;
    `
    }
});

(async () => {
    try {
        const response = await fetch(apiUrl);
        if (!response.ok) throw new Error(`HTTP error! Status: ${response.status}`);

        const data = await response.json();

        const layout = container.createEl('div', {
            attr: {
                style: `
                    margin-left: 1.5em;                   
                `
            }
        });

        const card = layout.createEl('div', {
            cls: 'random-curiosity',
        });

        card.createEl('p', {
            text: `${data.title}`,
            attr: {
                style: 'font-weight: bold; margin-bottom: 0.5em; font-size: 1.2em;'
            }
        });

        card.createEl('p', {
            text: `${data.text}`,
            attr: {
                style: 'margin: 0.4em 0; text-align: justify; text-justify: inter-word;'
            }
        });


    } catch (error) {
        container.createEl('p', {
            text: `❌ Couldn't load japanese word: ${error.message}`
        });
    }
})();
```

</div>

---

今日も一日頑張ってね (Ganbatte ne)!

<center><img src="https://imgur.com/rT548IP.gif" alt="Anna Yanami" width="400px"/></center>