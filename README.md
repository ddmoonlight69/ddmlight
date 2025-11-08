<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DD Moonlight - Artistic Muse & Digital Companion</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
            color: #fff;
            overflow-x: hidden;
        }

        /* Animated background particles */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            animation: float 20s infinite linear;
        }

        @keyframes float {
            from {
                transform: translateY(100vh) translateX(0);
            }
            to {
                transform: translateY(-100vh) translateX(100px);
            }
        }

        /* Header */
        header {
            position: relative;
            height: 100vh;
            display: flex;
            # DD Moonlight — static site

            This repository is a single-page static site. The canonical source is `index.html` (markup, styles and scripts).

            Quick preview (from repo root):

            ```bash
            python3 -m http.server 8000
            # then open http://localhost:8000/
            ```

            If you edit the site, prefer changing `index.html`. For larger refactors we extract CSS/JS into `styles.css` and `app.js` and update `index.html` accordingly.

            See `.github/copilot-instructions.md` for guidance aimed at automated coding agents and contributors.
