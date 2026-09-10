# Laycon
index.html
[VFX12 Final Graphics.html](https://github.com/user-attachments/files/32055708/VFX12.Final.Graphics.html)
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>LAYCON — Tactical HUD</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box
        }
        :root {
            --orange: #fb802b;
            --green: #528255;
            --black: #050705;
            --line: rgba(82, 130, 85, 0.28);
            --line-orange: rgba(251, 128, 43, 0.35)
        }
        html,
        body {
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
            overflow: hidden
        }
        body {
            min-height: 100vh;
            background: var(--black);
            color: var(--green);
            font-family: "Arial Narrow", "Roboto Condensed", "Helvetica Neue", Arial, sans-serif;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative
        }
        .row--footer-4.row--height-thin.js-row[data-rowtype="footer-4"],
        #page-zones__footer-widgets__691dceff13d2d-widgets__691dceff164dc,
        #page-zones__footer-widgets__691dceff13d2d-widgets__691dceff1c9c9 {
            display: none !important;
            visibility: hidden !important;
            opacity: 0 !important;
            pointer-events: none !important;
            height: 0 !important;
            width: 0 !important;
            overflow: hidden !important;
            position: absolute !important;
            top: -9999px !important;
            left: -9999px !important
        }
        .forest-background {
            position: fixed;
            inset: 0;
            z-index: 0;
            background-image: linear-gradient(rgba(0, 0, 0, .6), rgba(0, 0, 0, .74)), url("https://images.unsplash.com/photo-1448375240586-882707db888b?auto=format&fit=crop&w=2400&q=85");
            background-size: cover;
            background-position: center;
            filter: grayscale(100%) contrast(115%) hue-rotate(80deg) saturate(.8);
            transform: scale(1.04);
            transition: transform 2s ease, filter 2s ease
        }
        .forest-background::after {
            content: "";
            position: absolute;
            inset: 0;
            background: radial-gradient(circle at center, rgba(0, 0, 0, .08) 0, rgba(0, 0, 0, .58) 70%, rgba(0, 0, 0, .88) 100%)
        }
        body::before {
            content: "";
            position: fixed;
            inset: 0;
            pointer-events: none;
            opacity: .1;
            background: repeating-linear-gradient(0deg, rgba(255, 255, 255, .035) 0, rgba(255, 255, 255, .035) 1px, transparent 1px, transparent 4px);
            z-index: 100
        }
        body::after {
            content: "";
            position: fixed;
            inset: 0;
            pointer-events: none;
            background-image: linear-gradient(rgba(82, 130, 85, .025) 1px, transparent 1px), linear-gradient(90deg, rgba(82, 130, 85, .025) 1px, transparent 1px);
            background-size: 50px 50px;
            z-index: 1
        }
        .opening-overlay {
            position: fixed;
            inset: 0;
            z-index: 200;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: rgba(5, 7, 5, .92);
            backdrop-filter: blur(4px);
            pointer-events: none;
            animation: openingFade 2.9s cubic-bezier(.23, 1, .32, 1) forwards;
            transform-origin: center center;
        }
        .opening-overlay::before {
            content: "";
            position: absolute;
            inset: 0;
            background: radial-gradient(circle at center, rgba(251, 128, 43, .04) 0, transparent 70%);
            pointer-events: none
        }
        .opening-text .lay-part {
            color: #3a7a3a;
            text-shadow: 0 0 20px rgba(82, 130, 85, 0.3), 0 0 60px rgba(82, 130, 85, 0.2);
            -webkit-text-fill-color: #3a7a3a;
            background: 0 0;
            -webkit-background-clip: unset;
            background-clip: unset;
            font-weight: 900
        }
        .opening-text .con-part {
            color: #d96c1f;
            text-shadow: 0 0 20px rgba(251, 128, 43, 0.25), 0 0 60px rgba(251, 128, 43, 0.15);
            -webkit-text-fill-color: #d96c1f;
            background: 0 0;
            -webkit-background-clip: unset;
            background-clip: unset;
            font-weight: 900
        }
        .opening-sub .green-text {
            color: #3a7a3a;
            -webkit-text-fill-color: #3a7a3a;
            text-shadow: 0 0 12px rgba(82, 130, 85, 0.2);
            font-weight: 900
        }
        .opening-sub .orange-text,
        .opening-sub .orange-digit {
            color: #d96c1f;
            -webkit-text-fill-color: #d96c1f;
            text-shadow: 0 0 12px rgba(251, 128, 43, 0.2);
            font-weight: 900
        }
        .glow-line {
            position: absolute;
            left: 50%;
            top: 50%;
            width: 60%;
            height: 2px;
            transform: translateX(-50%);
            background: linear-gradient(90deg, transparent, #fb802b, #fb802b, transparent);
            box-shadow: 0 0 40px #fb802b, 0 0 80px #fb802b, 0 0 120px rgba(251, 128, 43, .4);
            opacity: 0;
            animation: glowFlash 2.9s ease forwards;
            z-index: 4;
            border-radius: 4px
        }
        .glow-line::after {
            content: "";
            position: absolute;
            top: 50%;
            left: 0;
            width: 100%;
            height: 30px;
            transform: translateY(-50%);
            background: radial-gradient(ellipse at center, rgba(251, 128, 43, .15) 0, transparent 70%);
            filter: blur(8px);
            pointer-events: none
        }
        @keyframes glowFlash {
            0% {
                opacity: 0;
                box-shadow: 0 0 10px #fb802b, 0 0 30px rgba(251, 128, 43, .1)
            }
            15% {
                opacity: 1;
                box-shadow: 0 0 50px #fb802b, 0 0 100px #fb802b, 0 0 150px rgba(251, 128, 43, .5)
            }
            35% {
                opacity: .9;
                box-shadow: 0 0 40px #fb802b, 0 0 80px #fb802b, 0 0 120px rgba(251, 128, 43, .4)
            }
            60% {
                opacity: .6;
                box-shadow: 0 0 20px #fb802b, 0 0 40px rgba(251, 128, 43, .2)
            }
            85% {
                opacity: .2;
                box-shadow: 0 0 10px #fb802b, 0 0 20px rgba(251, 128, 43, .1)
            }
            100% {
                opacity: 0;
                box-shadow: 0 0 0 transparent
            }
        }
        @keyframes openingFade {
            0% {
                opacity: 1;
                backdrop-filter: blur(4px);
                transform: scale(1);
            }
            65% {
                opacity: 1;
                backdrop-filter: blur(4px);
                transform: scale(1);
            }
            88% {
                opacity: 0.8;
                backdrop-filter: blur(8px);
                transform: scale(0.92);
            }
            100% {
                opacity: 0;
                backdrop-filter: blur(14px);
                visibility: hidden;
                pointer-events: none;
                background: transparent;
                transform: scale(0.85);
            }
        }
        .opening-text {
            position: relative;
            z-index: 5;
            font-size: clamp(1.1rem, 5.6vw, 2.4rem);
            font-weight: 900;
            letter-spacing: .3em;
            text-transform: uppercase;
            font-family: 'Arial Narrow', 'Roboto Condensed', sans-serif;
            padding: .2em .8em;
            border: 1px solid rgba(251, 128, 43, .25);
            border-radius: 8px;
            backdrop-filter: blur(2px);
            box-shadow: 0 0 60px rgba(251, 128, 43, .2);
            animation: textPulse 1.4s ease-in-out infinite alternate;
            letter-spacing: 8px;
            display: flex;
            flex-direction: row;
            gap: .1em;
            white-space: nowrap
        }
        .opening-sub {
            position: relative;
            z-index: 5;
            margin-top: .6rem;
            font-size: clamp(.55rem, 1.4vw, .9rem);
            letter-spacing: .04em;
            font-weight: 900;
            background: rgba(0, 0, 0, .3);
            padding: .3rem 1.6rem;
            font-family: 'Arial Narrow', sans-serif;
            backdrop-filter: blur(4px);
            text-align: center;
            line-height: 1.5;
            max-width: 95%;
            white-space: nowrap;
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: center;
            gap: .3em;
            flex-wrap: wrap;
            border: none
        }
        .opening-sub .glow-divider {
            display: inline-block;
            width: 2em;
            height: 2px;
            background: linear-gradient(90deg, transparent, #fb802b, #fb802b, transparent);
            box-shadow: 0 0 20px #fb802b, 0 0 40px #fb802b, 0 0 60px rgba(251, 128, 43, .3);
            border-radius: 4px;
            animation: flickerDivider .9s infinite alternate;
            flex-shrink: 0;
            margin: 0 .2em
        }
        .opening-sub .glow-divider-left {
            background: linear-gradient(90deg, transparent, #fb802b, #fb802b);
            box-shadow: 0 0 20px #fb802b, 0 0 40px #fb802b, 0 0 60px rgba(251, 128, 43, .3)
        }
        .opening-sub .glow-divider-right {
            background: linear-gradient(90deg, #fb802b, #fb802b, transparent);
            box-shadow: 0 0 20px #fb802b, 0 0 40px #fb802b, 0 0 60px rgba(251, 128, 43, .3)
        }
        @keyframes flickerDivider {
            0% {
                opacity: .5;
                box-shadow: 0 0 10px #fb802b, 0 0 25px rgba(251, 128, 43, .3)
            }
            30% {
                opacity: 1;
                box-shadow: 0 0 20px #fb802b, 0 0 50px #fb802b, 0 0 75px rgba(251, 128, 43, .5)
            }
            60% {
                opacity: .6;
                box-shadow: 0 0 15px #fb802b, 0 0 35px rgba(251, 128, 43, .4)
            }
            80% {
                opacity: 1;
                box-shadow: 0 0 25px #fb802b, 0 0 60px #fb802b, 0 0 90px rgba(251, 128, 43, .6)
            }
            100% {
                opacity: .8;
                box-shadow: 0 0 15px #fb802b, 0 0 40px rgba(251, 128, 43, .4)
            }
        }
        @keyframes textPulse {
            0% {
                text-shadow: 0 0 15px #fb802b, 0 0 40px #fb802b, 0 0 70px rgba(251, 128, 43, .4);
                opacity: .9
            }
            100% {
                text-shadow: 0 0 30px #fb802b, 0 0 80px #fb802b, 0 0 130px rgba(251, 128, 43, .7);
                opacity: 1
            }
        }
        #mainCompassWrapper {
            opacity: 0;
            animation: compassFadeIn 0.6s ease forwards 2.9s;
        }
        @keyframes compassFadeIn {
            0% {
                opacity: 0;
                transform: scale(0.92);
            }
            100% {
                opacity: 1;
                transform: scale(1);
            }
        }
        .compass.hidden {
            opacity: 0 !important;
            transform: scale(.7) !important;
            pointer-events: none !important;
        }
        header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 15px 30px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            z-index: 30;
            transition: opacity .7s ease, transform .8s ease
        }
        .logo {
            color: var(--green);
            font-size: 26px;
            font-weight: 900;
            letter-spacing: 5px;
            text-transform: uppercase;
            text-shadow: 0 0 15px rgba(0, 0, 0, .85);
            flex-shrink: 0;
            cursor: pointer
        }
        .logo span {
            color: var(--orange)
        }
        .command-strip {
            display: flex;
            align-items: center;
            gap: 3px;
            padding: 3px 6px;
            border: 1px solid rgba(82, 130, 85, .25);
            background: rgba(5, 7, 5, .62);
            backdrop-filter: blur(5px)
        }
        .command-strip::before {
            content: "COMMAND";
            display: flex;
            align-items: center;
            height: 24px;
            padding: 0 8px;
            color: rgba(82, 130, 85, .45);
            font-size: 6px;
            font-weight: 900;
            letter-spacing: 2px;
            border-right: 1px solid rgba(82, 130, 85, .22)
        }
        .command-link {
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 24px;
            padding: 0 10px;
            color: var(--green);
            text-decoration: none;
            font-size: 8.4px;
            font-weight: 900;
            letter-spacing: 1.44px;
            text-transform: uppercase;
            transition: color .25s ease, background .25s ease;
            cursor: default
        }
        .command-link::after {
            content: "";
            position: absolute;
            bottom: 0;
            left: 50%;
            width: 0;
            height: 1.5px;
            background: var(--orange);
            transform: translateX(-50%);
            transition: width .25s ease
        }
        .command-link:hover {
            color: var(--orange);
            background: rgba(251, 128, 43, .07)
        }
        .command-link:hover::after {
            width: 60%
        }
        main {
            position: fixed;
            inset: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 5;
            pointer-events: none
        }
        main .compass-wrapper {
            pointer-events: auto;
            position: relative;
            transition: all .5s cubic-bezier(.22, 1, .36, 1)
        }
        .compass {
            position: relative;
            width: min(48vw, 440px);
            height: min(48vw, 440px);
            filter: drop-shadow(0 18px 38px rgba(0, 0, 0, .72));
            transition: opacity .3s ease, transform .3s ease
        }
        .compass-face {
            position: absolute;
            inset: 0;
            border-radius: 50%;
            transform-origin: center center;
            display: flex;
            align-items: center;
            justify-content: center
        }
        .circle {
            position: absolute;
            border-radius: 50%;
            pointer-events: none;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%)
        }
        .circle-outer {
            width: 100%;
            height: 100%;
            border: 1px solid var(--line-orange);
            box-shadow: 0 0 30px rgba(251, 128, 43, .06)
        }
        .circle-inner {
            width: 86%;
            height: 86%;
            border: 1px solid var(--line)
        }
        .circle-middle {
            width: 56%;
            height: 56%;
            border: 1px solid var(--line)
        }
        .degree-ring {
            position: absolute;
            width: 96%;
            height: 96%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            pointer-events: none;
            z-index: 4;
            overflow: visible
        }
        .tick {
            position: absolute;
            width: 1px;
            height: 8px;
            background: rgba(82, 130, 85, .7);
            transform-origin: center center
        }
        .tick.major {
            width: 2px;
            height: 16px;
            background: var(--orange)
        }
        .windrose {
            position: absolute;
            width: 78%;
            height: 78%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            z-index: 2
        }
        .windrose::before {
            content: "";
            position: absolute;
            left: 50%;
            top: 3%;
            bottom: 3%;
            width: 1px;
            background: linear-gradient(transparent, var(--orange), transparent);
            transform: translateX(-50%);
            opacity: .75
        }
        .windrose::after {
            content: "";
            position: absolute;
            top: 50%;
            left: 3%;
            right: 3%;
            height: 1px;
            background: linear-gradient(transparent, var(--orange), transparent);
            transform: translateY(-50%);
            opacity: .75
        }
        .needle-container {
            position: absolute;
            left: 50%;
            top: 50%;
            width: 0;
            height: 0;
            z-index: 9;
            transform: translate(-50%, -50%) rotate(0deg);
            transform-origin: center center;
            transition: transform 1.15s cubic-bezier(.22, 1, .36, 1)
        }
        .needle {
            position: absolute;
            left: -3px;
            top: -135px;
            width: 6px;
            height: 270px;
            border-radius: 5px;
            background: linear-gradient(to bottom, var(--orange) 0, var(--orange) 47%, var(--green) 53%, var(--green) 100%);
            box-shadow: 0 0 12px rgba(251, 128, 43, .25)
        }
        .needle::before {
            content: "";
            position: absolute;
            left: 50%;
            top: -16px;
            width: 0;
            height: 0;
            transform: translateX(-50%);
            border-left: 8px solid transparent;
            border-right: 8px solid transparent;
            border-bottom: 22px solid var(--orange)
        }
        .needle::after {
            content: "";
            position: absolute;
            left: 50%;
            bottom: -16px;
            width: 0;
            height: 0;
            transform: translateX(-50%) rotate(180deg);
            border-left: 8px solid transparent;
            border-right: 8px solid transparent;
            border-bottom: 22px solid var(--green)
        }
        .direction {
            position: absolute;
            width: 120px;
            height: 120px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            text-decoration: none;
            color: var(--green);
            background: rgba(5, 7, 5, .86);
            border: 1px solid var(--line);
            transition: transform .4s ease, background .4s ease, border-color .4s ease, box-shadow .4s ease;
            z-index: 15
        }
        .direction:hover {
            color: var(--orange);
            background: rgba(251, 128, 43, .1);
            border-color: var(--orange);
            box-shadow: 0 0 35px rgba(251, 128, 43, .16)
        }
        .direction-content {
            width: 100%;
            max-width: 110px;
            text-align: center;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center
        }
        .direction-letter {
            display: block;
            color: var(--orange);
            font-size: 11px;
            font-weight: 900;
            letter-spacing: 3px;
            margin-bottom: 4px
        }
        .direction-title {
            display: block;
            width: 100%;
            color: var(--green);
            font-size: 11px;
            font-weight: 900;
            letter-spacing: 1px;
            text-transform: uppercase;
            white-space: nowrap
        }
        .direction-description {
            display: block;
            width: 100%;
            margin-top: 4px;
            color: var(--orange);
            font-size: 6.5px;
            font-weight: 900;
            line-height: 1.3;
            letter-spacing: .3px;
            text-align: center
        }
        .direction:hover .direction-title {
            color: var(--orange)
        }
        .north {
            top: -25px;
            left: 50%;
            transform: translateX(-50%)
        }
        .north:hover {
            transform: translateX(-50%) scale(1.08)
        }
        .east {
            right: -25px;
            top: 50%;
            transform: translateY(-50%)
        }
        .east:hover {
            transform: translateY(-50%) scale(1.08)
        }
        .south {
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%)
        }
        .south:hover {
            transform: translateX(-50%) scale(1.08)
        }
        .west {
            left: -25px;
            top: 50%;
            transform: translateY(-50%)
        }
        .west:hover {
            transform: translateY(-50%) scale(1.08)
        }
        .center {
            position: absolute;
            width: 90px;
            height: 90px;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            background: radial-gradient(circle, #182119, #080b08);
            border: 2px solid var(--orange);
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 30px rgba(251, 128, 43, .14);
            z-index: 20;
            cursor: pointer
        }
        .center::before {
            content: "";
            position: absolute;
            inset: 6px;
            border: 1px solid rgba(251, 128, 43, .3);
            border-radius: 50%
        }
        .center-text {
            position: relative;
            font-size: 18px;
            font-weight: 900;
            letter-spacing: 0;
            white-space: nowrap;
            text-transform: uppercase;
            z-index: 2
        }
        .center-text .lay {
            color: var(--green)
        }
        .center-text .con {
            color: var(--orange)
        }
        .status {
            position: fixed;
            left: 50%;
            bottom: 20px;
            transform: translateX(-50%);
            text-align: center;
            z-index: 25;
            transition: opacity .5s ease
        }
        .status-label {
            color: var(--green);
            font-size: 6px;
            font-weight: 900;
            letter-spacing: 3px;
            opacity: .6;
            text-transform: uppercase
        }
        .status-value {
            margin-top: 4px;
            color: var(--orange);
            font-size: 10px;
            font-weight: 900;
            letter-spacing: 3px;
            text-transform: uppercase
        }
        .corner {
            position: fixed;
            width: 25px;
            height: 25px;
            border-color: rgba(82, 130, 85, .45);
            z-index: 55;
            transition: opacity .5s ease
        }
        .corner-tl {
            top: 15px;
            left: 15px;
            border-top: 1px solid;
            border-left: 1px solid
        }
        .corner-tr {
            top: 15px;
            right: 15px;
            border-top: 1px solid;
            border-right: 1px solid
        }
        .corner-bl {
            bottom: 15px;
            left: 15px;
            border-bottom: 1px solid;
            border-left: 1px solid
        }
        .corner-br {
            bottom: 15px;
            right: 15px;
            border-bottom: 1px solid;
            border-right: 1px solid
        }
        .social-icons {
            position: fixed;
            left: 25px;
            bottom: 25px;
            z-index: 40;
            display: flex;
            flex-direction: column;
            gap: 12px;
            align-items: center
        }
        .social-icons a {
            display: block;
            width: 31px;
            height: 31px;
            transition: transform .2s ease
        }
        .social-icons a:hover {
            transform: scale(1.15)
        }
        .social-icons svg {
            width: 100%;
            height: 100%;
            fill: var(--orange)
        }
        .copyright {
            position: fixed;
            right: 20px;
            bottom: 20px;
            z-index: 40;
            font-size: 9px;
            font-weight: 900;
            letter-spacing: .5px;
            text-align: right;
            pointer-events: none;
            text-shadow: 0 2px 12px rgba(0, 0, 0, .9)
        }
        .copyright .green {
            color: var(--green)
        }
        .copyright .orange {
            color: var(--orange)
        }
        .walking-lines {
            position: fixed;
            inset: 0;
            z-index: 80;
            pointer-events: none;
            opacity: 0
        }
        .walking-lines::before,
        .walking-lines::after {
            content: "";
            position: absolute;
            left: 50%;
            width: 2px;
            height: 100vh;
            background: linear-gradient(to bottom, transparent, rgba(251, 128, 43, .55), transparent);
            opacity: 0
        }
        .walking-lines::before {
            transform: translateX(-120px)
        }
        .walking-lines::after {
            transform: translateX(120px)
        }
        body.walking .walking-lines {
            opacity: 1
        }
        body.walking .walking-lines::before {
            animation: walkLines .8s linear infinite
        }
        body.walking .walking-lines::after {
            animation: walkLines .8s linear infinite .2s
        }
        body.walking.walking-east .walking-lines::before,
        body.walking.walking-east .walking-lines::after,
        body.walking.walking-west .walking-lines::before,
        body.walking.walking-west .walking-lines::after {
            background: linear-gradient(to right, transparent, rgba(251, 128, 43, .55), transparent);
            height: 2px;
            width: 100vw;
            top: 50%;
            left: 0;
            transform: none;
            animation: walkLinesHorizontal .8s linear infinite
        }
        body.walking.walking-east .walking-lines::after,
        body.walking.walking-west .walking-lines::after {
            animation-delay: .2s
        }
        body.walking.walking-east .walking-lines::before,
        body.walking.walking-east .walking-lines::after {
            top: calc(50% - 120px)
        }
        body.walking.walking-west .walking-lines::before,
        body.walking.walking-west .walking-lines::after {
            top: calc(50% - 120px)
        }
        @keyframes walkLines {
            0% {
                transform: translate(-120px, -100%);
                opacity: 0
            }
            20% {
                opacity: .7
            }
            100% {
                transform: translate(-120px, 100%);
                opacity: 0
            }
        }
        @keyframes walkLinesHorizontal {
            0% {
                transform: translateX(-100%);
                opacity: 0
            }
            20% {
                opacity: .7
            }
            100% {
                transform: translateX(100%);
                opacity: 0
            }
        }
        .walking-message {
            position: fixed;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%) scale(.8);
            z-index: 90;
            text-align: center;
            pointer-events: none;
            opacity: 0
        }
        body.walking .walking-message {
            animation: walkingMessage 1.9s ease forwards
        }
        .walking-message-main {
            color: var(--orange);
            font-size: 14px;
            font-weight: 900;
            letter-spacing: 5px;
            text-transform: uppercase;
            text-shadow: 0 0 18px rgba(251, 128, 43, .35)
        }
        .walking-message-sub {
            margin-top: 8px;
            color: var(--green);
            font-size: 6px;
            font-weight: 900;
            letter-spacing: 3px;
            text-transform: uppercase
        }
        @keyframes walkingMessage {
            0% {
                opacity: 0;
                transform: translate(-50%, -50%) scale(.8)
            }
            20% {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1)
            }
            70% {
                opacity: 1
            }
            100% {
                opacity: 0;
                transform: translate(-50%, -65%) scale(1.05)
            }
        }
        .sub-compass-wrapper {
            position: fixed;
            inset: 0;
            z-index: 60;
            display: flex;
            align-items: center;
            justify-content: center;
            pointer-events: none;
            opacity: 0;
            transition: opacity .5s ease
        }
        .sub-compass-wrapper.active {
            opacity: 1;
            pointer-events: auto
        }
        .sub-compass-wrapper .compass {
            transform: scale(.92);
            opacity: 0;
            transition: transform .6s cubic-bezier(.22, 1, .36, 1), opacity .5s ease
        }
        .sub-compass-wrapper.active .compass {
            transform: scale(1);
            opacity: 1
        }
        .sub-direction {
            position: absolute;
            width: 120px;
            height: 120px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            text-decoration: none;
            color: var(--green);
            background: rgba(5, 7, 5, .86);
            border: 1px solid var(--line);
            transition: transform .4s ease, background .4s ease, border-color .4s ease, box-shadow .4s ease;
            z-index: 15;
            text-align: center;
            padding: 8px
        }
        .sub-direction:hover {
            color: var(--orange);
            background: rgba(251, 128, 43, .1);
            border-color: var(--orange);
            box-shadow: 0 0 35px rgba(251, 128, 43, .16);
            transform: scale(1.08)
        }
        .sub-direction .sub-dir-letter {
            display: block;
            color: var(--orange);
            font-size: 11px;
            font-weight: 900;
            letter-spacing: 3px;
            margin-bottom: 4px
        }
        .sub-direction .sub-dir-label {
            display: block;
            width: 100%;
            font-size: 11px;
            font-weight: 900;
            letter-spacing: 1px;
            text-transform: uppercase;
            line-height: 1.2;
            color: var(--green);
            word-break: break-word
        }
        .sub-direction .sub-dir-desc {
            display: block;
            width: 100%;
            font-size: 8px;
            font-weight: 900;
            letter-spacing: .5px;
            text-transform: uppercase;
            line-height: 1.2;
            color: var(--orange);
            word-break: break-word;
            margin-top: 2px
        }
        .sub-direction .sub-dir-sub {
            display: block;
            margin-top: 3px;
            color: var(--orange);
            font-size: 7px;
            font-weight: 900;
            letter-spacing: .5px;
            line-height: 1.2
        }
        .sub-direction:hover .sub-dir-label {
            color: var(--orange)
        }
        .sub-direction:hover .sub-dir-desc {
            color: var(--orange)
        }
        .sub-north {
            top: -25px;
            left: 50%;
            transform: translateX(-50%)
        }
        .sub-north:hover {
            transform: translateX(-50%) scale(1.08)
        }
        .sub-east {
            right: -25px;
            top: 50%;
            transform: translateY(-50%)
        }
        .sub-east:hover {
            transform: translateY(-50%) scale(1.08)
        }
        .sub-south {
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%)
        }
        .sub-south:hover {
            transform: translateX(-50%) scale(1.08)
        }
        .sub-west {
            left: -25px;
            top: 50%;
            transform: translateY(-50%)
        }
        .sub-west:hover {
            transform: translateY(-50%) scale(1.08)
        }
        .sub-center {
            position: absolute;
            width: 90px;
            height: 90px;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            border-radius: 50%;
            background: radial-gradient(circle, #182119, #080b08);
            border: 2px solid var(--orange);
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 30px rgba(251, 128, 43, .14);
            z-index: 20;
            cursor: pointer
        }
        .sub-center::before {
            content: "";
            position: absolute;
            inset: 6px;
            border: 1px solid rgba(251, 128, 43, .3);
            border-radius: 50%
        }
        .sub-center-text {
            position: relative;
            font-size: 18px;
            font-weight: 900;
            letter-spacing: 0;
            white-space: nowrap;
            text-transform: uppercase;
            z-index: 2;
            color: var(--green);
            text-align: center;
            line-height: 1.15
        }
        .page-coaching .sub-dir-label,
        .page-academy .sub-dir-label {
            font-size: 8.5px !important;
            letter-spacing: .2px !important;
            line-height: 1.2 !important
        }
        .page-coaching .sub-center-text {
            font-size: 14px !important
        }
        .page-academy .sub-center-text {
            font-size: 13px !important;
            letter-spacing: .5px !important
        }
        .back-button {
            position: fixed;
            left: 50%;
            bottom: 80px;
            width: 52px;
            height: 52px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
            background: var(--orange);
            border: 2px solid var(--orange);
            border-radius: 50%;
            cursor: pointer;
            z-index: 65;
            opacity: 0;
            pointer-events: none;
            transform: translate(-50%, 0);
            transition: opacity .5s ease, border-color .3s ease, background .3s ease, box-shadow .3s ease, transform .3s ease;
            box-shadow: 0 0 25px rgba(251, 128, 43, .3);
            text-decoration: none
        }
        .back-button.active {
            opacity: 1;
            pointer-events: auto
        }
        .back-button:hover {
            background: #e6731f;
            border-color: #e6731f;
            box-shadow: 0 0 40px rgba(251, 128, 43, .5);
            transform: translate(-50%, -2px)
        }
        .back-arrow {
            width: 26px;
            height: 26px;
            overflow: visible
        }
        .back-arrow-curve {
            fill: none;
            stroke: var(--black);
            stroke-width: 5;
            stroke-linecap: round
        }
        .back-arrow-head {
            fill: var(--black)
        }
        .module-detail {
            position: fixed;
            left: 25px;
            right: 25px;
            bottom: 25px;
            max-width: 620px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            padding: 22px 25px 20px;
            background: rgba(5, 7, 5, .96);
            border: 1px solid rgba(251, 128, 43, .35);
            box-shadow: 0 -15px 50px rgba(0, 0, 0, .45);
            transform: translateY(130%);
            opacity: 0;
            z-index: 70;
            transition: transform .55s cubic-bezier(.22, 1, .36, 1), opacity .45s ease;
            max-height: calc(100vh - 50px);
            min-height: 480px;
            pointer-events: none
        }
        .module-detail.open {
            transform: translateY(0);
            opacity: 1;
            pointer-events: auto
        }
        .module-detail-label {
            flex-shrink: 0;
            color: var(--orange);
            font-size: 7px;
            font-weight: 900;
            letter-spacing: 3px;
            text-transform: uppercase
        }
        .module-detail-title {
            flex-shrink: 0;
            margin-top: 8px;
            color: var(--orange);
            font-size: 22px;
            font-weight: 900;
            letter-spacing: 2px;
            text-transform: uppercase
        }
        .module-detail-text-wrapper {
            flex: 1 1 auto;
            min-height: 80px;
            max-height: 340px;
            overflow-y: auto;
            margin-top: 12px;
            padding-right: 8px;
            position: relative
        }
        .module-detail-text-wrapper::-webkit-scrollbar {
            width: 6px
        }
        .module-detail-text-wrapper::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, .06);
            border-radius: 10px
        }
        .module-detail-text-wrapper::-webkit-scrollbar-thumb {
            background: var(--orange);
            border-radius: 10px
        }
        .module-detail-text-wrapper {
            scrollbar-width: thin;
            scrollbar-color: var(--orange) rgba(255, 255, 255, .06)
        }
        .module-detail-text {
            color: rgba(235, 238, 235, .82);
            font-size: 11px;
            line-height: 1.7;
            font-weight: 700;
            -webkit-overflow-scrolling: touch
        }
        .module-detail-text p {
            margin: 0 0 12px
        }
        .module-detail-text p:last-child {
            margin-bottom: 0
        }
        .module-detail-text strong {
            color: var(--orange);
            font-weight: 900
        }
        .label-orange {
            color: var(--orange);
            font-weight: 900;
        }
        .label-green {
            color: var(--green);
            font-weight: 900;
        }
        .module-slideshow {
            flex-shrink: 0;
            margin-top: 18px;
            width: 100%;
            height: 220px;
            overflow: hidden;
            border: 1px solid rgba(82, 130, 85, .28);
            background: rgba(0, 0, 0, .35);
            position: relative
        }
        .module-slide video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
            background: #000;
        }
        .module-slide {
            position: absolute;
            inset: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
            opacity: 0;
            transform: translateX(20px);
            transition: opacity .45s ease, transform .45s ease;
            background: transparent;
            overflow: hidden;
        }
        .module-slide.active {
            opacity: 1;
            transform: translateX(0);
            z-index: 2;
        }
        .module-slide-dots {
            position: absolute;
            left: 50%;
            bottom: 9px;
            transform: translateX(-50%);
            display: flex;
            gap: 6px;
            z-index: 10;
        }
        .module-slide-dots span {
            width: 5px;
            height: 5px;
            border-radius: 50%;
            border: 1px solid var(--green);
            background: transparent;
            transition: background .2s;
        }
        .module-slide-dots span.active {
            background: var(--orange);
            border-color: var(--orange);
        }
        .module-detail-close {
            position: absolute;
            top: 12px;
            right: 15px;
            color: var(--orange);
            background: 0 0;
            border: none;
            font-size: 17px;
            cursor: pointer;
            z-index: 20;
        }
        .module-signup-button {
            flex-shrink: 0;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            margin-top: 16px;
            min-height: 25px;
            padding: 0 22px;
            color: var(--black);
            background: var(--orange);
            border: 1px solid var(--orange);
            font-family: inherit;
            font-size: 8px;
            font-weight: 900;
            letter-spacing: 2.5px;
            text-decoration: none;
            text-transform: uppercase;
            align-self: flex-start;
            cursor: pointer;
            transition: background .3s ease, color .3s ease;
            z-index: 10;
        }
        .module-signup-button:hover {
            background: transparent;
            color: var(--orange)
        }
        /* ---- responsive overrides ---- */
        @media(max-width:700px) {
            header {
                padding: 8px 10px;
                flex-direction: column;
                gap: 5px;
                align-items: center
            }
            .logo {
                font-size: 24px;
                letter-spacing: 4.5px
            }
            .command-strip {
                width: 100%;
                justify-content: center;
                padding: 5px 10px;
                flex-wrap: nowrap;
                overflow-x: auto;
                gap: 6px;
                border-radius: 4px
            }
            .command-strip::before {
                display: none
            }
            .command-link {
                flex: 0 0 auto;
                padding: 0 8px;
                font-size: 8.4px;
                letter-spacing: .38px;
                height: 28px;
                color: var(--green)
            }
            .command-link::after {
                height: 2px
            }
            .compass {
                width: 88.4vw;
                height: 88.4vw;
                margin: 0 auto
            }
            .compass-face {
                display: flex;
                align-items: center;
                justify-content: center
            }
            .circle-outer {
                width: 100% !important;
                height: 100% !important
            }
            .circle-inner {
                width: 86% !important;
                height: 86% !important
            }
            .circle-middle {
                width: 56% !important;
                height: 56% !important
            }
            .degree-ring {
                width: 96% !important;
                height: 96% !important;
                top: 50% !important;
                left: 50% !important;
                transform: translate(-50%, -50%) !important
            }
            .tick {
                height: 6.5px !important;
                width: 1.3px !important
            }
            .tick.major {
                height: 13px !important;
                width: 1.95px !important
            }
            .direction,
            .sub-direction {
                width: 93.6px;
                height: 93.6px
            }
            .direction-content {
                max-width: 83.2px
            }
            .direction-letter,
            .sub-direction .sub-dir-letter {
                font-size: 9.1px;
                margin-bottom: 2.6px;
                letter-spacing: 1.95px
            }
            .direction-title {
                font-size: 9.1px;
                letter-spacing: .26px;
                color: var(--green)
            }
            .sub-direction .sub-dir-label {
                font-size: 9.1px;
                letter-spacing: .26px;
                color: var(--green)
            }
            .sub-direction .sub-dir-desc {
                font-size: 6.5px;
                letter-spacing: .3px;
                color: var(--orange)
            }
            .sub-direction .sub-dir-sub {
                font-size: 6px;
                margin-top: 2px
            }
            .direction-description {
                font-size: 5.85px;
                line-height: 1.3;
                margin-top: 2.6px
            }
            .north,
            .sub-north {
                top: -7.8px
            }
            .east,
            .sub-east {
                right: -7.8px
            }
            .south,
            .sub-south {
                bottom: -7.8px
            }
            .west,
            .sub-west {
                left: -7.8px
            }
            .center,
            .sub-center {
                width: 65px;
                height: 65px
            }
            .center-text {
                font-size: 14.04px
            }
            .sub-center-text {
                font-size: 14.04px
            }
            .needle {
                height: 195px;
                top: -97.5px;
                width: 5.2px
            }
            .needle::before {
                border-left-width: 5.2px;
                border-right-width: 5.2px;
                border-bottom-width: 18.2px;
                top: -13px
            }
            .needle::after {
                border-left-width: 5.2px;
                border-right-width: 5.2px;
                border-bottom-width: 18.2px;
                bottom: -13px
            }
            .corner {
                width: 12px;
                height: 12px
            }
            .corner-tl,
            .corner-tr {
                top: 8px
            }
            .corner-bl,
            .corner-br {
                bottom: 8px
            }
            .corner-tl,
            .corner-bl {
                left: 8px
            }
            .corner-tr,
            .corner-br {
                right: 8px
            }
            .social-icons {
                left: 18px;
                bottom: 18px;
                gap: 10px
            }
            .social-icons a {
                width: 31px;
                height: 31px
            }
            .copyright {
                right: 23px;
                bottom: 10px;
                font-size: 7px;
                letter-spacing: .4px
            }
            .status {
                bottom: 10px
            }
            .status-label {
                font-size: 7.2px;
                letter-spacing: 3.6px
            }
            .status-value {
                font-size: 12px;
                letter-spacing: 3.6px;
                margin-top: 4.8px
            }
            body.walking .compass {
                transform: translateY(110vh) scale(1.15) rotate(4deg)
            }
            body.walking.walking-east .compass {
                transform: translateX(110vw) scale(1.15) rotate(6deg)
            }
            body.walking.walking-west .compass {
                transform: translateX(-110vw) scale(1.15) rotate(-6deg)
            }
            .walking-message-main {
                font-size: 8px;
                letter-spacing: 2px
            }
            .walking-message-sub {
                font-size: 4px;
                letter-spacing: 1.5px
            }
            .opening-text {
                letter-spacing: 4px;
                font-size: clamp(.9rem, 4.4vw, 1.8rem);
                white-space: nowrap
            }
            .opening-sub {
                font-size: clamp(.4rem, 1.1vw, .65rem);
                padding: .2rem .8rem;
                line-height: 1.4;
                white-space: normal;
                max-width: 95%;
                flex-wrap: wrap;
                gap: .2em
            }
            .glow-line {
                width: 80%;
                top: 50%
            }
            .back-button {
                bottom: 60px;
                width: 44px;
                height: 44px
            }
            .back-arrow {
                width: 22px;
                height: 22px
            }
            .module-detail {
                left: 15px;
                right: 15px;
                bottom: 15px;
                max-width: none;
                padding: 16px 16px 18px;
                max-height: calc(100dvh - 30px);
                min-height: 340px;
                border-radius: 0
            }
            .module-detail-title {
                font-size: 17px;
                margin-top: 6px;
                padding-right: 30px;
                color: var(--orange)
            }
            .module-detail-text-wrapper {
                min-height: 70px;
                max-height: 255px;
                margin-top: 10px
            }
            .module-detail-text {
                font-size: 10px;
                line-height: 1.65
            }
            .module-slideshow {
                height: 180px;
                margin-top: 14px
            }
            .module-signup-button {
                width: 100%;
                min-height: 29px;
                margin-top: 14px;
                justify-content: center
            }
            .module-detail-close {
                top: 12px;
                right: 14px;
                font-size: 20px;
                padding: 6px
            }
            .module-detail-text-wrapper::-webkit-scrollbar {
                width: 4px
            }
            .page-coaching .sub-east .sub-dir-label,
            .page-coaching .sub-west .sub-dir-label {
                font-size: 7.2px !important;
                letter-spacing: 0 !important
            }
            .page-coaching .sub-center-text {
                font-size: 12px !important
            }
            .page-academy .sub-center-text {
                font-size: 11px !important;
                letter-spacing: 0 !important
            }
        }
        @media(max-width:380px) {
            .direction,
            .sub-direction {
                width: 75.4px;
                height: 75.4px
            }
            .direction-content {
                max-width: 65px
            }
            .direction-title {
                font-size: 7.8px;
                color: var(--green)
            }
            .sub-direction .sub-dir-label {
                font-size: 7.8px;
                color: var(--green)
            }
            .sub-direction .sub-dir-desc {
                font-size: 6px;
                color: var(--orange)
            }
            .sub-direction .sub-dir-sub {
                font-size: 5.5px
            }
            .direction-description {
                font-size: 5.2px;
                line-height: 1.3
            }
            .center,
            .sub-center {
                width: 54.6px;
                height: 54.6px
            }
            .center-text {
                font-size: 10.92px
            }
            .sub-center-text {
                font-size: 10.92px
            }
            .needle {
                height: 156px;
                top: -78px
            }
            .compass {
                width: 80.6vw;
                height: 80.6vw
            }
            .social-icons {
                left: 16px;
                bottom: 16px;
                gap: 8px
            }
            .social-icons a {
                width: 28px;
                height: 28px
            }
            .copyright {
                right: 23px;
                font-size: 6px
            }
            .glow-line {
                width: 85%;
                top: 48%
            }
            .opening-text {
                font-size: clamp(.8rem, 3.6vw, 1.4rem);
                letter-spacing: 3px;
                white-space: nowrap
            }
            .opening-sub {
                font-size: clamp(.35rem, 1vw, .55rem);
                padding: .2rem .6rem;
                white-space: normal
            }
            .back-button {
                width: 38px;
                height: 38px;
                bottom: 50px
            }
            .back-arrow {
                width: 19px;
                height: 19px
            }
            .module-slideshow {
                height: 160px
            }
            .module-detail-text-wrapper {
                max-height: 200px;
                min-height: 60px
            }
            .module-detail {
                min-height: 280px
            }
            .page-coaching .sub-east .sub-dir-label,
            .page-coaching .sub-west .sub-dir-label {
                font-size: 6.5px !important
            }
            .page-coaching .sub-center-text {
                font-size: 10px !important
            }
            .page-academy .sub-center-text {
                font-size: 10px !important
            }
        }
        @media(min-width:701px) and (max-width:1024px) {
            .compass {
                width: 55vw;
                height: 55vw
            }
            .direction,
            .sub-direction {
                width: 95px;
                height: 95px
            }
            .direction-content {
                max-width: 85px
            }
            .direction-title {
                font-size: 9px;
                color: var(--green)
            }
            .sub-direction .sub-dir-label {
                font-size: 9px;
                color: var(--green)
            }
            .sub-direction .sub-dir-desc {
                font-size: 7px;
                color: var(--orange)
            }
            .sub-direction .sub-dir-sub {
                font-size: 6.5px
            }
            .direction-description {
                font-size: 5.5px;
                line-height: 1.3
            }
            .north,
            .sub-north {
                top: -15px
            }
            .east,
            .sub-east {
                right: -15px
            }
            .south,
            .sub-south {
                bottom: -15px
            }
            .west,
            .sub-west {
                left: -15px
            }
            .center,
            .sub-center {
                width: 70px;
                height: 70px
            }
            .center-text {
                font-size: 14.4px
            }
            .sub-center-text {
                font-size: 14.4px
            }
            .needle {
                height: 200px;
                top: -100px
            }
            .glow-line {
                width: 70%;
                top: 50%
            }
            .opening-text {
                font-size: clamp(1.4rem, 4vw, 2.4rem);
                white-space: nowrap
            }
            .opening-sub {
                font-size: clamp(.5rem, 1.1vw, .7rem);
                white-space: nowrap;
                gap: .3em
            }
            .module-detail-text-wrapper {
                max-height: 306px;
                min-height: 80px
            }
            .module-detail {
                min-height: 440px
            }
            .page-coaching .sub-east .sub-dir-label,
            .page-coaching .sub-west .sub-dir-label {
                font-size: 7.8px !important
            }
            .page-coaching .sub-center-text {
                font-size: 13px !important
            }
            .page-academy .sub-center-text {
                font-size: 12px !important
            }
        }
        @media(min-width:1025px) {
            .opening-text {
                font-size: clamp(1.9rem, 4.8vw, 3rem);
                letter-spacing: 10px;
                white-space: nowrap
            }
            .opening-sub {
                margin-top: .5rem;
                font-size: clamp(.65rem, 1.3vw, 1rem);
                padding: .2rem 2rem;
                white-space: nowrap;
                letter-spacing: .06em;
                gap: .3em;
                flex-wrap: nowrap
            }
            .glow-line {
                width: 55%;
                top: 50%
            }
            .module-detail-text-wrapper {
                max-height: 340px;
                min-height: 80px
            }
        }
    </style>
</head>
<body>
    <div class="forest-background"></div>
    <div class="opening-overlay" id="openingOverlay">
        <div class="glow-line"></div>
        <div class="opening-text"><span class="lay-part">LAY</span><span class="con-part">CON</span></div>
        <div class="opening-sub"><span class="green-text">Zoals men ijzer scherpt met ijzer</span><span class="glow-divider glow-divider-left"></span><span class="orange-text">Spreuken </span><span class="orange-digit">27:17</span><span class="glow-divider glow-divider-right"></span><span class="green-text">zo scherpt een mens zijn medemens</span></div>
    </div>
    <div class="walking-lines"></div>
    <div class="walking-message">
        <div class="walking-message-main" id="walkingMessageMain">NORTH // COACHING</div>
        <div class="walking-message-sub" id="walkingMessageSub">ROUTE INITIALIZED — MOVING NORTH</div>
    </div>
    <div class="corner corner-tl"></div>
    <div class="corner corner-tr"></div>
    <div class="corner corner-bl"></div>
    <div class="corner corner-br"></div>
    <header>
        <div class="logo" id="homeLogo">LAY<span>CON</span></div>
        <nav class="command-strip">
            <span class="command-link">Info</span>
            <span class="command-link">Overige</span>
            <span class="command-link">Over mij</span>
            <span class="command-link">Contact</span>
            <span class="command-link">Tarieven</span>
        </nav>
    </header>
    <main>
        <div class="compass-wrapper" id="mainCompassWrapper">
            <div class="compass" id="mainCompass">
                <div class="compass-face">
                    <div class="circle circle-outer"></div>
                    <div class="circle circle-inner"></div>
                    <div class="circle circle-middle"></div>
                    <div class="degree-ring" id="degreeRing"></div>
                    <div class="windrose"></div>
                    <div class="needle-container" id="needle">
                        <div class="needle"></div>
                    </div>
                    <div class="direction north" data-angle="0" data-title="Coaching" data-page="coaching">
                        <div class="direction-content"><span class="direction-letter">N</span><span class="direction-title">COACHING</span><span class="direction-description">PERSOONLIJK &amp; ONTWIKKELING</span></div>
                    </div>
                    <div class="direction east" data-angle="90" data-title="Workshops" data-page="workshops">
                        <div class="direction-content"><span class="direction-letter">E</span><span class="direction-title">WORKSHOPS</span><span class="direction-description">ERVARING &amp; PLEZIER</span></div>
                    </div>
                    <div class="direction south" data-angle="180" data-title="Bivak" data-page="bivak">
                        <div class="direction-content"><span class="direction-letter">S</span><span class="direction-title">BIVAK</span><span class="direction-description">AVONTUUR &amp; VERBINDING</span></div>
                    </div>
                    <div class="direction west" data-angle="270" data-title="Academy" data-page="academy">
                        <div class="direction-content"><span class="direction-letter">W</span><span class="direction-title">ACADEMY</span><span class="direction-description">ZELFBESCHERMING &amp; HOME DEFENSE</span></div>
                    </div>
                    <div class="center" id="homeCenter">
                        <div class="center-text"><span class="lay">LAY</span><span class="con">CON</span></div>
                    </div>
                </div>
            </div>
        </div>
        <div class="status">
            <div class="status-label">Current selection</div>
            <div class="status-value" id="statusValue">Coaching</div>
        </div>
    </main>
    <div class="sub-compass-wrapper" id="subCompassWrapper">
        <div class="compass" id="subCompass">
            <div class="compass-face">
                <div class="circle circle-outer"></div>
                <div class="circle circle-inner"></div>
                <div class="circle circle-middle"></div>
                <div class="degree-ring" id="subDegreeRing"></div>
                <div class="windrose"></div>
                <div class="needle-container" id="subNeedle">
                    <div class="needle"></div>
                </div>
                <div id="subDirectionsContainer"></div>
                <div class="sub-center" id="subCenter">
                    <div class="sub-center-text" id="subCenterText">Coaching</div>
                </div>
            </div>
        </div>
    </div>
    <button class="back-button" id="backButton" aria-label="Terug naar het hoofdkompas">
        <svg class="back-arrow" viewBox="0 0 60 60" xmlns="http://www.w3.org/2000/svg">
            <path class="back-arrow-curve" d="M44 42C44 24, 28 14, 16 22"></path>
            <path class="back-arrow-head" d="M6 22L17 14L17 30Z"></path>
        </svg>
    </button>
    <div class="module-detail" id="moduleDetail">
        <button class="module-detail-close" id="moduleDetailClose">×</button>
        <div class="module-detail-label" id="detailLabel">Module // Selected</div>
        <div class="module-detail-title" id="detailTitle">Module Title</div>
        <div class="module-detail-text-wrapper" id="detailTextWrapper">
            <div class="module-detail-text" id="detailText"></div>
        </div>
        <div class="module-slideshow" id="moduleSlideshow">
            <div class="module-slide active" data-slide="0">
                <video playsinline webkit-playsinline muted preload="auto"></video>
            </div>
            <div class="module-slide" data-slide="1">
                <video playsinline webkit-playsinline muted preload="auto"></video>
            </div>
            <div class="module-slide" data-slide="2">
                <video playsinline webkit-playsinline muted preload="auto"></video>
            </div>
            <div class="module-slide-dots"><span class="active"></span><span></span><span></span></div>
        </div>
        <button class="module-signup-button" id="detailSignupBtn">AANMELDEN</button>
    </div>
    <div class="social-icons">
        <a href="https://www.youtube.com/@LAYCONCOACHING" target="_blank" aria-label="YouTube"><svg viewBox="0 0 24 24"><path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg></a>
        <a href="https://www.instagram.com/layconcoaching/" target="_blank" aria-label="Instagram"><svg viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/></svg></a>
    </div>
    <div class="copyright"><span class="green">LAYCON</span> <span class="orange">©</span> <span class="green">- KVK 77166019</span></div>
    <script>
        // ---- PAGE_DATA with videos per direction ----
        const PAGE_DATA = {
            coaching: {
                title: "Coaching",
                centerText: "Coaching",
                items: [{
                    label: "Identiteit & onzekerheid",
                    desc: "Ben jij op zoek naar jezelf? Of merk je dat je soms moeite hebt in je dagelijks leven omdat je onzekerheid ervaart? Door middel van identiteitsvorming ontdek je wat voor jou belangrijk is, en met weerbaarheidstraining krijg je tools om jezelf beter te beschermen. Samen zorgen we ervoor dat jij krachtig en zelfverzekerd in het leven staat.",
                    thema: "Kracht & Zelfbescherming",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/8106396/8106396-uhd_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/4824740/4824740-uhd_2560_1440_30fps.mp4",
                        "https://videos.pexels.com/video-files/4100360/4100360-uhd_2732_1440_25fps.mp4"
                    ]
                }, {
                    label: "Discipline & Zelfstandigheid",
                    desc: "Stop ermee om je eigen vijand te zijn, het is tijd voor actie! Als het gaat over discipline, dan zeggen we eigenlijk doorzetten. Mag jouw vuurtje harder branden en weet je dat je het kunt, maar heb je iemand nodig die naast je staat en je motiveert? In dit onderdeel van coaching focussen we op het inplannen van je tijd, het beheren van je financiën, of het nemen van eigen beslissingen over onderwerpen waar jij jezelf te kort doet. Discipline kunnen we combineren met sport, en Zelfstandigheid om jouw persoonlijk leven een boost te geven!",
                    thema: "Discipline & Zelfstandigheid",
                    doelgroep: "Jongeren / Volwassenen",
                    deelname: "Individuele coaching",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/31916408/13595184_2560_1440_30fps.mp4",
                        "https://videos.pexels.com/video-files/6963830/6963830-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/8489172/8489172-hd_1920_1080_30fps.mp4"
                    ]
                }, {
                    label: "Motivatie & Richting",
                    desc: "Behoefte aan goede verdiepende gesprekken, en wil jij de richting van jouw levenskompas opnieuw bepalen omdat je verdwaald geraakt bent? Samen gaan we kijken waar je tegen aan loopt, en hoe jij op de plek kan komen waar je wil zijn. We werken aan het versterken van je motivatie, zodat je niet alleen begint, maar ook door gaat. Door bewust stil te staan bij je waarden en verlangens, creëren we een duidelijke richting die jou helpt om keuzes te maken die echt bij je passen.",
                    thema: "Motivatie & Richting",
                    doelgroep: "Jongeren / Volwassenen",
                    deelname: "Individuele coaching",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/8120852/8120852-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/34633230/14679030_2560_1440_30fps.mp4",
                        "https://videos.pexels.com/video-files/38022683/16138207_2730_1440_25fps.mp4"
                    ]
                }, {
                    label: "GEDRAGSCOACHING SCHOOL & THUIS",
                    desc: "Met gedragscoaching maak ik je bewust van je gedrag en ga ik de confrontatie met je aan. Maar belangrijker nog, we gaan samen kijken wat de onderliggende reden eigenlijk echt is waardoor jij bepaald gedrag hebt wat afwijkt van wat wenselijk is. Zit je eigenlijk wel lekker in je vel? Of sta je onder een verwachtingspatroon van je omgeving en beïnvloed dit jouw keuzes. Ben je eigenlijk wel bewust van de gevolgen die het voor jou persoonlijk zal hebben op de langere termijn? In deze coaching staan verbinding, innerlijke strijd en het afsluiten van patronen centraal.",
                    thema: "Gedrag & Lifestyle",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "Individuele coaching",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/7698998/7698998-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/6935705/6935705-hd_1920_1080_30fps.mp4",
                        "https://videos.pexels.com/video-files/32099451/13684423_1920_1080_30fps.mp4"
                    ]
                }]
            },
            workshops: {
                title: "Workshops",
                centerText: "Workshops",
                items: [{
                    label: "Bushcraft & Survival",
                    desc: "Survival gaat over overleven, in een situatie waar voor je niet gekozen hebt en waarschijnlijk ook niet op gerekend hebt. Wat doe je? Hoe werk je goed samen en welke dingen zijn het belangrijk. Bij Bushcraft kies je er juist wél voor het bos in te gaan, en het met minder te doen dan wat je gewend bent. Lijkt het je leuk om overlevingsskills te leren?\n\nInhoud - Deze workshop bestaat uit een reeks opvolgende basistechnieken die worden aangeleerd. Het bouwen van (natuurlijke) onderkomens, vuur maken, waterfilteren, wandelen met een kompas, boogschieten behoren allemaal tot de basis. Natuurlijk is het mogelijk om verdieping toe te passen; in de verdieping behandelen we jagen, eetbare wilde planten, tactisch overleven, EHBO in het veld, SOS-signalen, MORSE-codes, communicatie enzovoorts.\n\nLocatie - Deze workshop laat zich het best geven in een natuurlijke omgeving met voorkeur voor een bosrijke omgeving. Indien het niet mogelijk is, is een sportveld met enkele bomen ook mogelijk.\nToepassing - De workshop is erg uitgebreid en biedt tal van mogelijkheden, we horen daarom graag wat de wensen zijn. Workshops zijn vaak 1 á 2 uren per les, de mogelijkheden zijn om er een dagdeel aan te besteden. Indien je kijkt naar een mogelijkheid voor een schoolreisje of kinderfeest, navigeer dan richting Bivak op de startpagina.",
                    thema: "Overleven - Natuur - Zelfredzaamheid",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/9292893/9292893-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/37685506/15978189_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/5029843/5029843-uhd_2732_1440_30fps.mp4"
                    ]
                }, {
                    label: "Real life gaming",
                    desc: "Vanaf een leeftijd van 8 jaar kan je samen met je team Real Life Gamen. Alle spelvormen kunnen op locatie gegeven worden, waarbij je zelf alvast voorbereidingen kan doen voor camouflage, beschutting of met je team plannen kan smeden om je overwinning te behalen. Gaan jullie voor een team-match of liever free-for-all?\n\nLocatie - Real Life Gaming kan het beste op buitenterreinen gespeeld worden zoals in bosgebied, stedelijk gebied of grasvelden. Als toevoeging kunnen we afhankelijk van de speeltijd tijd reserveren om camouflage toe te passen d.m.v. camo-netting en camo-paint, en natuurlijk het bouwen van je basecamp, het camoufleren van je blaster en eventueel een ghillie-suit voor een maximaal tactische gameplay behoort ook tot de mogelijkheden.\n\nBlasters - Schieten doe je met gel-balletjes, geschikt voor kinderen. Uiteraard zijn onze gel-balletjes biologisch afbreekbaar, net als de rookgranaten en zijn deze niet giftig voor mens en omgeving. Ammo is in principe onbeperkt voor de maximale speelbeleving.\n\nToepassing - Afhankelijk van de speelruimte kunnen we spellen organiseren tot maximaal 30 personen. Natuurlijk staat veiligheid en verantwoorde omgang met elkaar en materiaal centraal tijdens het spelen.\n\nVoorzieningen – Jullie worden voorzien van volledig gezichtsbescherming en Blasters. Als toevoeging kunnen we jullie gear uitbreiden met camouflage netten, rookgranaten en eventueel de mogelijkheid om extra wapens in het veld te veroveren!\n\nTijd - Deze workshop is zowel mogelijk voor scholen als kinderfeestjes en duurt gemiddeld 2 tot 3 uur met een pauze en verschillende spelvormen.",
                    thema: "Plezier – Activiteit - Samenwerken",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 30 personen",
                    leeftijd: "> 8 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/5607632/5607632-uhd_2732_1440_24fps.mp4",
                        "https://videos.pexels.com/video-files/13721790/13721790-hd_1920_1080_60fps.mp4",
                        "https://videos.pexels.com/video-files/30892854/13208153_2560_1440_60fps.mp4"
                    ]
                }, {
                    label: "Short Films",
                    desc: "Kun je een goed verhaal verzinnen? Mooi! Dan beginnen we met het schrijven van een script en rolverdeling. Daarna gaan we scenes oefenen en locatie's bezoeken en kijken hoe alles over moet komen op de kijker. Als alles rond is, gaan we daadwerkelijk filmen en acteren. Begint je creatieve brein al te draaien? En ben je dan een indiaan die verdwaalde jongeren de weg wijst in het bos? Of breken jullie in in je eigen school om de gevangen meester te redden? Deze workshop vraagt toewijding en motivatie, want uiteindelijk rolt er een product uit wat jullie zelf gemaakt en bedacht hebben! Een mooi moment om later op terug te kijken, of een maatschappelijke boodschap te geven aan jullie omgeving d.m.v. een Short Film.\n\nLocatie – Deze workshop komt naar je toe en zal gefilmd worden in en rondom de school.\n\nTijd – De ervaring is dat een Short Film van 10 minuten minimaal 10 lessen van 2 uur in beslag neemt.",
                    thema: "Creativiteit",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 10 personen",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/9810158/9810158-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/9303797/9303797-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/5877872/5877872-uhd_2560_1440_30fps.mp4"
                    ]
                }, {
                    label: "Kickbox & Bootcamp",
                    desc: "Met Kickbox leer je verdedigen, aanvallen en combinatie aanvallen. Ook ga je sparren met elkaar en onderzoek je of dit wellicht iets is voor jou om mee door te gaan in je eigen tijd. Je leert dat niet elke persoon minder sterk is dan jij. Heb je al ervaring, ook dan neem ik je graag mee in deze Workshop! Bootcamp brengt jou naar een next-level. Buiten, ja, ook als het regent en koud is. Ontdek jezelf en kijk hoe fit jij bent en wilt worden en ga de strijd aan met jezelf om jezelf te overwinnen!\n\nVolwassenen – Bootcamp trainingen zijn er om jou uit je comfortzone te trekken en dat nemen we bij LAYCON serieus. Trainingen kunnen dus ook in de late avond en de nacht gegeven worden. Sta jij om 02:00 uur klaar om te gaan rammen terwijl heel Nederland slaapt?\n\nLocatie – Buiten (rondom de school of afgesproken locatie)\n\nTijd – Lessen duren tussen de 1 en 2 uur.",
                    thema: "Ontspanning door Inspanning – Zelfverdediging – Discipline",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/38444006/16324859_1920_1080_50fps.mp4",
                        "https://videos.pexels.com/video-files/4987397/4987397-hd_1920_1080_30fps.mp4",
                        "https://videos.pexels.com/video-files/4964650/4964650-hd_1920_1080_25fps.mp4"
                    ]
                }]
            },
            bivak: {
                title: "Bivak",
                centerText: "Bivak",
                items: [{
                    label: "Ouder-kind bivak",
                    desc: "Bivak is geschikt voor ouders met kinderen vanaf een jaar of 6. Bivakkeren kan erg veel ontspanning meebrengen, bijvoorbeeld bij scheidingsproblematiek, stress, depressie, burnout etc. Bivakkeren trekt je even helemaal uit je normale omgeving, en de rust van de natuur maar ook de uitdaging om te zorgen voor eten en onderdak in de natuur doet daar een schepje bovenop. Wil je juist werken aan de relatie tussen ouder en kind omdat je elkaar 'kwijt' bent geraakt, dan is bivak ook zeker voor jullie! Of je nu kiest voor herstel en ontspanning, activiteiten en samenwerken, of gewoon even wil vluchten uit de dagelijkse omgeving, bivakkeren met jouw kind is een beleving voor jullie beiden!\n\nInhoud – Tijdens de bivak krijg je opdrachten. Natuurlijk is een plek om te slapen heel belangrijk, maar ook het navigeren met een kompas naar de plek waar je wil slapen. Onder leiding van LAYCON bepalen we samen de veiligheidsonderdelen, maar grotendeels krijgen jullie de mogelijkheid om naar eigen wens te bivakkeren. Andere opdrachten worden duidelijk op de locatie, wanneer jullie gesetteld zijn, en zijn afhankelijk of jullie willen inzetten op rust of activiteiten.\n\nMateriaal - Over spullen hoef je je geen zorgen te maken, al ons materiaal is van militaire kwaliteit. Hebben jullie zelf spullen, dan is dat natuurlijk mogelijk om deze te gebruiken!\n\nSetting - De mogelijkheid is er om zelf als derde persoon je kind te observeren terwijl het kind leert en ontspant (passieve rol), maar ook kunnen jullie samen opdrachten krijgen en dus beiden een actieve rol bekleden. De mogelijkheid bestaat om dit voor meerdere nachten te doen! Graag vernemen wij wat jij als ouder graag zou willen.\n\nNood – Alle rugzakken zijn voorzien van EHBO-pakketten. Hierin zit de basis, zoals verband en pleisters. Voor noodgevallen draagt iedereen ook een tourniquet, en is er alcohol aanwezig voor ontsmetting en Betadine-zalf. Ook draagt iedereen een hoofdlamp.\n\nVeiligheid op locatie – De locatie waar dit plaats zal vinden, zal onder voorbehoud van toestemming van Staatsbosbeheer gegeven worden, of van de eigenaar van het stuk grond. We zullen u en uw kind niet in onveiligheid brengen door te verwachten dieren op het terrein. Verder scannen we de locatie op bereikbaarheid van overige burgers.\n\nPersoonlijke veiligheid – Omdat wij de inschatting niet volledig kunnen maken wat er in jullie gezinssituatie speelt, vragen wij je om achtergrondinformatie te delen indien noodzakelijk. Deze afweging maak je zelf, maar bij betrokkenheid van veiligheidsinstanties (politie etc.) vragen wij je dit altijd te doen. Wij begrijpen bij LAYCON dat hoog opgelopen conflicten kunnen zorgen voor ongewenste situaties, en kijken graag met jou samen om de ervaring plezierig te maken voor jou en uw kind(eren).\n\nEten – Wij vragen jullie om zelf voorbereidingen te doen op basis van eten omdat wij geen rekening kunnen houden met allerlei wensen en beperkingen. Het voedsel zal boven het vuur klaargemaakt worden; denk hierbij dus aan barbecue-maaltijden of soep met brood. Ook de tussendoortjes en drinken zijn voor jullie eigen verantwoordelijkheid. Maak er dus een feestje van! LAYCON zorgt ervoor dat er altijd extra water aanwezig is op locatie.\n\nMedicatie – Gebruik jij of jouw kind medicatie? Zorg er dan voor dat je hierover nadenkt om dit mee te nemen voor de lengte die jullie bivakkeren.\n\nLocatie – Buiten (privéterrein of bosgebied)\n\nTijd – >24 uur met een maximum van 100 uur aaneengesloten bivakkeren",
                    thema: "Herstel – Verbinding - Ontspanning",
                    doelgroep: "Ouder – Kind combinatie",
                    deelname: "< 4",
                    leeftijd: "> 6",
                    videos: [
                        "https://videos.pexels.com/video-files/10420166/10420166-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/6133260/6133260-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/6133101/6133101-uhd_2732_1440_25fps.mp4"
                    ]
                }, {
                    label: "Jongeren bivak",
                    desc: "Gaan jullie als groep samen in het bos slapen? Niet een feest tussen de bomen, maar een tactische setting met opdrachten om te leren overleven in de natuur? De opdrachten en materialen krijgen jullie van LAYCON, slaapzakken nemen jullie zelf mee. Ook deze Bivak is mogelijk als schoolreis en dus meerdaags; indien de groep groter is dan 10 personen, vragen wij je om even contact op te nemen i.v.m. de veiligheidswaarborging van de deelnemers. Samen gaan we voor succes, ervaring en buiten zijn!\n\nMateriaal – Het is de bedoeling dat iedereen zijn eigen slaapzak en luchtmat meeneemt in een rugzak.\n\nSetting – Tactisch, stealth: het doel is opgaan in de natuur. Het wordt dus geen feest met muziek; we respecteren de natuur en handelen volgens het LEAVE NO TRACE-principe.\n\nNood – LAYCON zal zorgen voor de basis voor EHBO inclusief tourniquetten.\n\nVeiligheid op locatie – De locatie waar dit plaats zal vinden, zal onder voorbehoud van toestemming van Staatsbosbeheer gegeven worden, of van de eigenaar van het stuk grond. We zullen jou en jouw groep niet in onveiligheid brengen door te verwachten dieren op het terrein. Verder scannen we de locatie op bereikbaarheid van overige burgers.\n\nAlgemene veiligheid – Wij verwachten persoonlijke toewijding en beoordelen of de deelnemers veilig met bijlen en messen kunnen werken. Wij behouden ons altijd het recht dit te onthouden aan bepaalde deelnemers. Wij vragen jullie om de groep zelf ook te beoordelen op medische achtergrond, psychische klachten of gedrag.\n\nEten – Wij vragen jullie om zelf voorbereidingen te doen op basis van eten omdat wij geen rekening kunnen houden met allerlei wensen en beperkingen. Het voedsel zal boven het vuur klaargemaakt worden; denk hierbij dus aan barbecue-maaltijden of soep met brood. Ook de tussendoortjes en drinken zijn voor jullie eigen verantwoordelijkheid. Maak er dus een feestje van! LAYCON zorgt ervoor dat er altijd extra water aanwezig is op locatie.\n\nMedicatie – Gebruik jij of een van de deelnemers medicatie? Zorg er dan voor dat je hierover nadenkt en kenbaar maakt aan de deelnemers om dit mee te nemen voor de lengte die jullie bivakkeren.\n\nGroepsveiligheid – Wij vragen om per 10 jongeren minimaal 2 volwassenen toe te voegen die de groep kennen. Indien er een mix van jongens en meisjes deelnemen, is het wenselijk om een vrouw toe te voegen als volwassene indien mogelijk.\n\nLocatie – Buiten (privéterrein of bosgebied)\n\nTijd – >24 uur met een maximum van 100 uur aaneengesloten bivakkeren",
                    thema: "Groepsvorming – Verbinding - Avontuur",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 12 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/31902801/13589439_2560_1440_60fps.mp4",
                        "https://videos.pexels.com/video-files/8968538/8968538-uhd_2732_1440_24fps.mp4",
                        "https://videos.pexels.com/video-files/36694034/15554794_2560_1440_60fps.mp4"
                    ]
                }, {
                    label: "VOLWASSENEN BIVAK",
                    desc: "Deze Bivak gaat heel het jaar rond. Dat betekent dat buiten slapen met -10 graden mogelijk is. In deze Bivak zetten we in op informatie en kennis, maar ook op tactisch handelen, planning en organisatie. Ook is de mogelijkheid er om de moeilijkheidsgraad te verhogen, door een maximum aan materialen af te spreken. Samen gaan we voor succes, ervaring en buiten zijn!\n\nMateriaal – Het is de bedoeling dat iedereen zijn eigen slaapzak en luchtmat meeneemt in een rugzak.\n\nSetting – Tactisch, stealth: het doel is opgaan in de natuur. We respecteren de natuur en handelen volgens het LEAVE NO TRACE-principe.\n\nNood – LAYCON zal zorgen voor de basis voor EHBO inclusief tourniquetten.\n\nVeiligheid op locatie – De locatie waar dit plaats zal vinden, zal onder voorbehoud van toestemming van Staatsbosbeheer gegeven worden, of van de eigenaar van het stuk grond. We zullen je niet in onveiligheid brengen door te verwachten dieren op het terrein. Verder scannen we de locatie op bereikbaarheid van overige burgers.\n\nAlgemene veiligheid – Wij verwachten persoonlijke toewijding en beoordelen of de deelnemers veilig met bijlen en messen kunnen werken. Wij behouden ons altijd het recht dit te onthouden aan bepaalde deelnemers. Wij vragen jullie zelf ook te beoordelen op medische achtergrond, psychische klachten of fysieke beperking.\n\nEten – Wij vragen jullie om zelf voorbereidingen te doen op basis van eten omdat wij geen rekening kunnen houden met allerlei wensen en beperkingen. Het voedsel zal boven het vuur klaargemaakt worden; denk hierbij dus aan barbecue-maaltijden of soep met brood. Ook de tussendoortjes en drinken zijn voor jullie eigen verantwoordelijkheid. Maak er dus een feestje van! LAYCON zorgt ervoor dat er altijd extra water aanwezig is op locatie.\n\nMedicatie – Gebruikt iemand medicatie? Zorg er dan voor dat iedereen hierover nadenkt om dit mee te nemen voor de lengte van deelname.\n\nLocatie – Buiten (privéterrein of bosgebied)\n\nTijd – >24 uur met een maximum van 100 uur aaneengesloten bivakkeren",
                    thema: "Karaktervorming – Natuur - Kennis",
                    doelgroep: "Volwassenen",
                    deelname: "< 10 personen",
                    leeftijd: "> 18 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/6200851/6200851-uhd_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/13633676/13633676-uhd_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/36693904/15554734_2560_1440_60fps.mp4"
                    ]
                }, {
                    label: "Bivak training",
                    desc: "Deze Bivak gaat heel het jaar rond. Dat betekent dat buiten slapen met -10 graden mogelijk is. In deze Bivak zetten we in op informatie en kennis, maar ook op tactisch handelen, planning en organisatie. Ook is de mogelijkheid er om de moeilijkheidsgraad te verhogen, door een maximum aan materialen af te spreken. Samen gaan we voor succes, ervaring en buiten zijn!\n\nMateriaal – Het is de bedoeling dat iedereen zijn eigen slaapzak en luchtmat meeneemt in een rugzak.\n\nSetting – Tactisch, stealth: het doel is opgaan in de natuur. We respecteren de natuur en handelen volgens het LEAVE NO TRACE-principe.\n\nNood – LAYCON zal zorgen voor de basis voor EHBO inclusief tourniquetten.\n\nVeiligheid op locatie – De locatie waar dit plaats zal vinden, zal onder voorbehoud van toestemming van Staatsbosbeheer gegeven worden, of van de eigenaar van het stuk grond. We zullen je niet in onveiligheid brengen door te verwachten dieren op het terrein. Verder scannen we de locatie op bereikbaarheid van overige burgers.\n\nAlgemene veiligheid – Wij verwachten persoonlijke toewijding en beoordelen of de deelnemers veilig met bijlen en messen kunnen werken. Wij behouden ons altijd het recht dit te onthouden aan bepaalde deelnemers. Wij vragen jullie zelf ook te beoordelen op medische achtergrond, psychische klachten of fysieke beperking.\n\nGroepsveiligheid – Wij vragen om per 10 jongeren minimaal 2 volwassenen toe te voegen die de groep kennen. Indien er een mix van jongens en meisjes deelnemen, is het wenselijk om een vrouw toe te voegen als volwassene indien mogelijk.\n\nEten – Wij vragen jullie om zelf voorbereidingen te doen op basis van eten omdat wij geen rekening kunnen houden met allerlei wensen en beperkingen. Het voedsel zal boven het vuur klaargemaakt worden; denk hierbij dus aan barbecue-maaltijden of soep met brood. Ook de tussendoortjes en drinken zijn voor jullie eigen verantwoordelijkheid. Maak er dus een feestje van! LAYCON zorgt ervoor dat er altijd extra water aanwezig is op locatie.\n\nMedicatie – Gebruikt iemand medicatie? Zorg er dan voor dat iedereen hierover nadenkt om dit mee te nemen voor de lengte van deelname.\n\nLocatie – Buiten (privéterrein of bosgebied)\n\nTijd – >24 uur met een maximum van 100 uur aaneengesloten bivakkeren",
                    thema: "Training – Natuur - Kennis",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 10 personen",
                    leeftijd: "> 12 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/36693904/15554734_2560_1440_60fps.mp4",
                        "https://videos.pexels.com/video-files/30909161/13215034_2560_1440_30fps.mp4",
                        "https://videos.pexels.com/video-files/5450130/5450130-uhd_2560_1440_30fps.mp4"
                    ]
                }]
            },
            academy: {
                title: "Academy",
                centerText: "Academy",
                items: [{
                    label: "Mentale weerbaarheid",
                    desc: "Hoe weerbaar ben jij wanneer er situaties op je afkomen die je vervelend of moeilijk zijn? Hoe handel jij onder stress, druk of emotie? Ben je tevreden met jezelf, en accepteer jij jezelf? Wanneer we het hebben over mentale weerbaarheid, neemt LAYCON je graag mee in gesprekken waar lastige vraagstukken besproken worden. Je leert afwegen en keuzes maken op basis van wat voor jou het beste is op dat moment. Wijsheid en inzicht staan centraal, maar ook acceptatie en loslaten. Afhankelijk van jouw leeftijd en hulpvragen versterken we jouw mentale positie. Thema's zoals groepsdruk, loverboys, seksuele intimidatie, zelfdiscipline, vertrouwen, onzekerheid en identiteit komen in deze ACADEMY voor.",
                    thema: "Mentale Weerbaarheid",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/8410278/8410278-hd_1920_1080_25fps.mp4",
                        "https://videos.pexels.com/video-files/8344644/8344644-uhd_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/4824821/4824821-uhd_2560_1440_30fps.mp4"
                    ]
                }, {
                    label: "Fysieke weerbaarheid",
                    desc: "Echt even rammen! Alles eruit gooien en met spierpijn op de bank liggen, dat ga je hier investeren in jezelf. Het doel is om jou lichamelijk meer weerbaar te maken, en je een mindset bij te brengen dat opgeven niet altijd nodig is wanneer jouw hoofd dat zegt! Niet fit? Dan gaan we daarmee aan het werk! Geen zin? Dan gaan we zin maken! Doorzetten en over de drempel heen is de standaard.\n\nIn deze ACADEMY behandelen we ook thema's zoals veiligheid op straat, handelen wanneer iemand je bedreigt met een wapen. Het bevat onderdelen van Judo, Krav Maga en MMA.",
                    thema: "Fysieke Weerbaarheid",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 10 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/8343375/8343375-uhd_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/38631563/16407987_2560_1440_60fps.mp4",
                        "https://videos.pexels.com/video-files/15779218/15779218-hd_1920_1080_25fps.mp4"
                    ]
                }, {
                    label: "Online weerbaarheid",
                    desc: "We leven in een aparte wereld, een wereld waar gevaren soms dichterbij zijn dan je denkt. Zeker met social media en online games is het bereiken van kinderen en jongeren ontzettend gemakkelijk geworden. Geloof het of niet, maar het ronselen van kinderen begint al op de leeftijd van 8 jaar. Daarbij is het platform Roblox een van de plekken waar dit het meest gebeurt, naast Snapchat. We hebben ook de afgelopen jaren een extreme stijging gezien in kinderhandel. Zelfbescherming en bewustwording voor jongere kinderen, over waar de grenzen liggen voor hun online gedrag, is absoluut noodzakelijk. We gaan het hebben over de daadwerkelijke gevaren op korte en langere termijn in deze online omgevingen, en daarbij ook wat het gedrag zou moeten zijn om jezelf te beschermen. Zelfbescherming, identiteit en grenzen staan hier centraal.",
                    thema: "Online Weerbaarheid - Zelfbescherming",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 8 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/7701946/7701946-uhd_2732_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/6269162/6269162-uhd_2560_1440_24fps.mp4",
                        "https://videos.pexels.com/video-files/7698902/7698902-uhd_2732_1440_25fps.mp4"
                    ]
                }, {
                    label: "HOME DEFENSE",
                    desc: "Ben jij wel eens alleen thuis en woon je niet in een hele veilige buurt? Of kom je in het donker wel eens alleen thuis van een avondje met vriendinnen en voel je je op dat moment onveilig? Home Defense gaat over het beschermen van jezelf, je gezin en je huis. In deze training leer je praktische vaardigheden op het gebied van thuisveiligheid, situationeel bewustzijn en hoe je moet handelen in noodsituaties. \n\nWe behandelen onderwerpen zoals het herkennen van verdachte situaties, het beveiligen van je woning, en hoe je effectief kunt communiceren in stressvolle omstandigheden. Ook is er de mogelijkheid om te trainen met wapens die gebruikt kunnen worden voor zelfverdediging; de kennis om deze te gebruiken en te plaatsen in de woning is ook onderdeel van deze training. Deze training is geschikt voor iedereen vanaf 12 jaar die zich veiliger wil voelen in en rondom zijn of haar eigen huis.",
                    thema: "Veiligheid – Zelfbescherming - Herkenning",
                    doelgroep: "Jongeren / Leerlingen",
                    deelname: "< 15 personen",
                    leeftijd: "> 12 jaar",
                    videos: [
                        "https://videos.pexels.com/video-files/8419554/8419554-hd_1920_1080_30fps.mp4",
                        "https://videos.pexels.com/video-files/7407142/7407142-uhd_2560_1440_25fps.mp4",
                        "https://videos.pexels.com/video-files/7231261/7231261-uhd_2560_1440_25fps.mp4"
                    ]
                }]
            }
        };

        // ---- existing compass variables (unchanged) ----
        const SUB_POSITIONS = [{ cls: 'sub-north', angle: 0, letter: 'N' }, { cls: 'sub-east', angle: 90, letter: 'E' }, { cls: 'sub-south', angle: 180, letter: 'S' }, { cls: 'sub-west', angle: 270, letter: 'W' }];

        const mainNeedle = document.getElementById("needle"),
            mainDegreeRing = document.getElementById("degreeRing"),
            mainDirections = document.querySelectorAll(".direction"),
            statusValue = document.getElementById("statusValue"),
            walkingMessageMain = document.getElementById("walkingMessageMain"),
            walkingMessageSub = document.getElementById("walkingMessageSub"),
            mainCompass = document.getElementById("mainCompass"),
            subCompassWrapper = document.getElementById("subCompassWrapper"),
            subNeedle = document.getElementById("subNeedle"),
            subDegreeRing = document.getElementById("subDegreeRing"),
            subCenterText = document.getElementById("subCenterText"),
            subDirectionsContainer = document.getElementById("subDirectionsContainer"),
            backButton = document.getElementById("backButton"),
            homeLogo = document.getElementById("homeLogo"),
            homeCenter = document.getElementById("homeCenter"),
            moduleDetail = document.getElementById("moduleDetail"),
            moduleDetailClose = document.getElementById("moduleDetailClose"),
            detailLabel = document.getElementById("detailLabel"),
            detailTitle = document.getElementById("detailTitle"),
            detailText = document.getElementById("detailText"),
            detailSignupBtn = document.getElementById("detailSignupBtn"),
            moduleSlides = document.querySelectorAll(".module-slide"),
            moduleSlideDots = document.querySelectorAll(".module-slide-dots span");

        let mainNeedleRotation = 0,
            subNeedleRotation = 0,
            isWalking = false,
            currentPage = null,
            activeSlide = 0;

        // ---- video slideshow control variables ----
        let slideshowTimeout = null;
        let slideshowEndedListener = null;
        let currentVideo = null;

        // ---- existing functions (unchanged) ----
        function buildDegreeRing(ring) {
            if (!ring) return;
            ring.innerHTML = '';
            const rect = ring.getBoundingClientRect(),
                size = rect.width || 400,
                radius = size * .48,
                centerX = size / 2,
                centerY = size / 2;
            for (let i = 0; i < 72; i++) {
                const tick = document.createElement("div");
                tick.classList.add("tick");
                if (i % 9 === 0) tick.classList.add("major");
                const angle = i * 5 * Math.PI / 180,
                    x = centerX + radius * Math.sin(angle),
                    y = centerY - radius * Math.cos(angle);
                tick.style.left = x / size * 100 + '%';
                tick.style.top = y / size * 100 + '%';
                tick.style.transform = 'translate(-50%,-50%) rotate(' + i * 5 + 'deg)';
                tick.style.transformOrigin = 'center center';
                ring.appendChild(tick)
            }
        }
        setTimeout(() => { buildDegreeRing(mainDegreeRing);
            buildDegreeRing(subDegreeRing) }, 100);
        let resizeTimer;
        window.addEventListener('resize', function() {
            clearTimeout(resizeTimer);
            resizeTimer = setTimeout(function() { buildDegreeRing(mainDegreeRing);
                buildDegreeRing(subDegreeRing) }, 150)
        });

        function moveMainNeedle(angle) {
            let target = Number(angle);
            while (target - mainNeedleRotation > 180) target -= 360;
            while (target - mainNeedleRotation < -180) target += 360;
            mainNeedleRotation = target;
            mainNeedle.style.transform = 'translate(-50%,-50%) rotate(' + mainNeedleRotation + 'deg)'
        }

        function moveSubNeedle(angle) {
            let target = Number(angle);
            while (target - subNeedleRotation > 180) target -= 360;
            while (target - subNeedleRotation < -180) target += 360;
            subNeedleRotation = target;
            subNeedle.style.transform = 'translate(-50%,-50%) rotate(' + subNeedleRotation + 'deg)'
        }

        // ---- slideshow UI update ----
        function showSlide(index) {
            if (!moduleSlides.length) return;
            activeSlide = (index + moduleSlides.length) % moduleSlides.length;
            moduleSlides.forEach((slide, i) => { slide.classList.toggle('active', i === activeSlide) });
            moduleSlideDots.forEach((dot, i) => { dot.classList.toggle('active', i === activeSlide) });
        }

        // ---- update video sources ----
        function updateSlideshowVideos(videos) {
            moduleSlides.forEach((slide, i) => {
                const video = slide.querySelector('video');
                if (video && videos && videos[i]) {
                    video.src = videos[i];
                    video.load(); // preload for faster start
                }
            });
        }

        // ---- video playback control ----
        function stopCurrentVideo() {
            if (slideshowTimeout) {
                clearTimeout(slideshowTimeout);
                slideshowTimeout = null;
            }
            if (slideshowEndedListener && currentVideo) {
                currentVideo.removeEventListener('ended', slideshowEndedListener);
                slideshowEndedListener = null;
            }
            if (currentVideo) {
                currentVideo.pause();
                currentVideo.currentTime = 0;
                currentVideo = null;
            }
            // also pause all other videos
            moduleSlides.forEach(slide => {
                const vid = slide.querySelector('video');
                if (vid && vid !== currentVideo) {
                    vid.pause();
                }
            });
        }

        function playSlide(index) {
            stopCurrentVideo(); // clean up previous

            const slide = moduleSlides[index];
            if (!slide) return;
            const video = slide.querySelector('video');
            if (!video || !video.src) {
                // if no src, skip to next after a short delay
                slideshowTimeout = setTimeout(() => {
                    moveToNextSlide();
                }, 1000);
                return;
            }

            currentVideo = video;
            video.currentTime = 0;
            video.play().catch(e => { /* ignore autoplay errors */ });

            slideshowTimeout = setTimeout(() => {
                moveToNextSlide();
            }, 15000);

            slideshowEndedListener = function() {
                if (slideshowTimeout) {
                    clearTimeout(slideshowTimeout);
                    slideshowTimeout = null;
                }
                moveToNextSlide();
            };
            video.addEventListener('ended', slideshowEndedListener);
        }

        function moveToNextSlide() {
            stopCurrentVideo();
            const next = (activeSlide + 1) % moduleSlides.length;
            showSlide(next);
            playSlide(next);
        }

        function startSlideshow() {
            stopCurrentVideo();
            // ensure all videos are paused and reset
            moduleSlides.forEach(slide => {
                const vid = slide.querySelector('video');
                if (vid) {
                    vid.pause();
                    vid.currentTime = 0;
                }
            });
            showSlide(0);
            playSlide(0);
        }

        function stopSlideshow() {
            stopCurrentVideo();
            moduleSlides.forEach(slide => {
                const vid = slide.querySelector('video');
                if (vid) vid.pause();
            });
        }

        // ---- existing helper functions (unchanged) ----
        function formatDescription(desc) {
            const lines = desc.split('\n');
            const processed = lines.map(line => {
                const match = line.match(/^([A-Za-z\s]+)\s[-–]/);
                if (match) {
                    const heading = match[1].trim();
                    const rest = line.substring(match[0].length);
                    return `<span class="label-green">${heading}</span> ${rest}`;
                }
                return line;
            });
            return processed.join('\n');
        }

        function formatTitle(pageKey, label) {
            if (pageKey === 'bivak') {
                if (label.toUpperCase().includes('VOLWASSENEN BIVAK')) {
                    const parts = label.split(' ');
                    if (parts.length === 2 && parts[1].toUpperCase() === 'BIVAK') {
                        return `<span style="color:var(--orange);">${parts[0]}</span> <span style="color:var(--green);">${parts[1]}</span>`;
                    }
                }
                const words = label.split(' ');
                const colored = words.map(w => {
                    if (w.toUpperCase() === 'BIVAK') {
                        return `<span style="color:var(--green);">${w}</span>`;
                    } else {
                        return `<span style="color:var(--orange);">${w}</span>`;
                    }
                });
                return colored.join(' ');
            }
            if (pageKey === 'academy') {
                const words = label.split(' ');
                const colored = words.map(w => {
                    if (w.toUpperCase() === 'WEERBAARHEID' || w.toUpperCase() === 'DEFENSE') {
                        return `<span style="color:var(--green);">${w}</span>`;
                    } else {
                        return `<span style="color:var(--orange);">${w}</span>`;
                    }
                });
                return colored.join(' ');
            }
            if (pageKey === 'workshops') {
                if (label.toLowerCase() === 'real life gaming') {
                    return `<span style="color:#108ea5;">REAL</span> <span style="color:#e3ac51;">LIFE</span> <span style="color:#d32074;">GAMING</span>`;
                }
                const words = label.split(' ');
                const colored = words.map(w => {
                    const upper = w.toUpperCase();
                    if (upper === 'SURVIVAL' || upper === 'FILMS' || upper === 'BOOTCAMP') {
                        return `<span style="color:var(--green);">${w}</span>`;
                    } else {
                        return `<span style="color:var(--orange);">${w}</span>`;
                    }
                });
                return colored.join(' ');
            }
            if (pageKey === 'coaching') {
                const words = label.split(' ');
                const colored = words.map(w => {
                    const lower = w.toLowerCase();
                    if (lower === 'school' || lower === '&' || lower === 'thuis' || lower === 'onzekerheid' ||
                        lower === 'zelfstandigheid' || lower === 'richting') {
                        return `<span style="color:var(--green);">${w}</span>`;
                    } else {
                        return `<span style="color:var(--orange);">${w}</span>`;
                    }
                });
                return colored.join(' ');
            }
            return `<span style="color:var(--orange);">${label}</span>`;
        }

        // ---- build sub compass (unchanged) ----
        function buildSubCompass(pageKey) {
            const data = PAGE_DATA[pageKey];
            if (!data) return;
            currentPage = pageKey;
            subCompassWrapper.className = 'sub-compass-wrapper active page-' + pageKey;

            if (pageKey === 'workshops') {
                subCenterText.innerHTML = '<span style="color:var(--orange);">WORK</span><br>SHOPS';
                subCenterText.style.fontSize = '';
            } else if (pageKey === 'coaching') {
                subCenterText.textContent = 'COACHING';
                subCenterText.style.fontSize = '';
            } else if (pageKey === 'academy') {
                subCenterText.textContent = 'ACADEMY';
                subCenterText.style.fontSize = '';
            } else {
                subCenterText.textContent = data.centerText.toUpperCase();
                subCenterText.style.fontSize = '';
            }

            subDirectionsContainer.innerHTML = '';
            const items = data.items;
            SUB_POSITIONS.forEach((pos, index) => {
                const item = items[index] || { label: 'Item', thema: '', doelgroep: '', deelname: '', leeftijd: '' };
                const btn = document.createElement('div');
                btn.className = 'sub-direction ' + pos.cls;
                btn.dataset.angle = pos.angle;
                btn.dataset.index = index;
                let labelText = item.label,
                    subText = '',
                    descText = '';
                if (pageKey === 'bivak') {
                    labelText = 'BIVAK';
                    const descMap = { N: 'OUDER - KIND', E: 'JONGEREN', S: 'VOLWASSENEN', W: 'TRAINING' };
                    const ageMap = { N: '6+', E: '12+', S: '18+', W: '12+' };
                    descText = descMap[pos.letter] || '';
                    subText = ageMap[pos.letter] || ''
                } else if (pageKey === 'workshops') {
                    const ageMap = { N: '10+', E: '8+', S: '10+', W: '10+' };
                    subText = ageMap[pos.letter] || ''
                } else if (pageKey === 'coaching') {
                    const ageMap = { N: '10+', E: '10+', S: '10+', W: '10+' };
                    subText = ageMap[pos.letter] || ''
                } else if (pageKey === 'academy') {
                    const ageMap = { N: '10+', E: '10+', S: '10+', W: '12+' };
                    subText = ageMap[pos.letter] || ''
                }
                let innerHTML = '<div class="direction-content"><span class="sub-dir-letter">' + pos.letter + '</span><span class="sub-dir-label">' + labelText + '</span>';
                if (descText) innerHTML += '<span class="sub-dir-desc">' + descText + '</span>';
                if (subText) innerHTML += '<span class="sub-dir-sub">' + subText + '</span>';
                innerHTML += '</div>';
                btn.innerHTML = innerHTML;
                subDirectionsContainer.appendChild(btn);
                btn.addEventListener('mouseenter', function() { moveSubNeedle(pos.angle) });
                btn.addEventListener('touchstart', function() { moveSubNeedle(pos.angle) }, { passive: true });
                btn.addEventListener('click', function() { openModuleDetail(pageKey, index) })
            });
            moveSubNeedle(0)
        }

        // ---- open module detail (with video slideshow) ----
        function openModuleDetail(pageKey, index) {
            const data = PAGE_DATA[pageKey];
            if (!data || !data.items[index]) return;
            const item = data.items[index];
            detailLabel.textContent = data.title + ' ' + String(index + 1).padStart(2, '0') + ' // Selected';
            detailTitle.innerHTML = formatTitle(pageKey, item.label);

            let formattedDesc = formatDescription(item.desc);
            if (pageKey === 'workshops' && index === 1) {
                formattedDesc = formattedDesc.replace(/\bBlasters\b/g, '<span style="color:#d32074;">Blasters</span>');
            }
            formattedDesc = formattedDesc.replace(/\n/g, '<br>');
            let html = '<p>' + formattedDesc + '</p>';
            html += '<p><span class="label-orange">Thema</span> — ' + item.thema + '</p>';
            html += '<p><span class="label-orange">Doelgroep</span> — ' + item.doelgroep + '</p>';
            html += '<p><span class="label-orange">Deelname</span> — ' + item.deelname + '</p>';
            html += '<p><span class="label-orange">Leeftijd</span> — ' + item.leeftijd + '</p>';
            detailText.innerHTML = html;

            // Update video slideshow with the item's videos
            if (item.videos && item.videos.length) {
                updateSlideshowVideos(item.videos);
            } else {
                // fallback: clear sources
                moduleSlides.forEach(slide => {
                    const vid = slide.querySelector('video');
                    if (vid) vid.src = '';
                });
            }

            moduleDetail.classList.add('open');
            // start video slideshow
            startSlideshow();
        }

        function closeModuleDetail() {
            moduleDetail.classList.remove('open');
            stopSlideshow();
        }

        moduleDetailClose.addEventListener('click', closeModuleDetail);
        document.addEventListener('keydown', function(e) { if (e.key === 'Escape') closeModuleDetail() });

        // ---- mailto signup (unchanged) ----
        detailSignupBtn.addEventListener('click', function() {
            window.location.href = 'mailto:info@laycon.nl?subject=Aanmelding%20LAYCON%20module';
            closeModuleDetail()
        });

        // ---- navigation (unchanged) ----
        function goToPage(pageKey) {
            if (isWalking) return;
            const data = PAGE_DATA[pageKey];
            if (!data) return;
            isWalking = true;
            mainCompass.classList.add('hidden');
            const dirMap = { coaching: 'NORTH', workshops: 'EAST', bivak: 'SOUTH', academy: 'WEST' };
            walkingMessageMain.textContent = (dirMap[pageKey] || '') + ' // ' + data.title.toUpperCase();
            walkingMessageSub.textContent = 'ROUTE INITIALIZED — MOVING ' + (dirMap[pageKey] || '');
            statusValue.textContent = (dirMap[pageKey] || '') + ' // ' + data.title;
            setTimeout(function() {
                document.body.classList.add("walking");
                if (pageKey === 'workshops' || pageKey === 'academy') { document.body.classList.add(pageKey === 'workshops' ? 'walking-east' : 'walking-west') }
            }, 200);
            setTimeout(function() {
                document.body.classList.remove("walking");
                document.body.classList.remove('walking-east', 'walking-west');
                isWalking = false;
                buildSubCompass(pageKey);
                subCompassWrapper.classList.add('active');
                backButton.classList.add('active');
                walkingMessageMain.textContent = (dirMap[pageKey] || '') + ' // ' + data.title.toUpperCase();
                walkingMessageSub.textContent = 'ARRIVED — ' + data.title.toUpperCase()
            }, 1900)
        }

        function goHome() {
            closeModuleDetail();
            subCompassWrapper.classList.remove('active');
            subCompassWrapper.className = 'sub-compass-wrapper';
            backButton.classList.remove('active');
            mainCompass.classList.remove('hidden');
            statusValue.textContent = 'Coaching';
            moveMainNeedle(0);
            currentPage = null
        }

        mainDirections.forEach(dir => {
            const angle = Number(dir.dataset.angle),
                title = dir.dataset.title,
                pageKey = dir.dataset.page;
            dir.addEventListener('mouseenter', function() { if (!isWalking && !subCompassWrapper.classList.contains(
                    'active')) { moveMainNeedle(angle);
                    statusValue.textContent = title } });
            dir.addEventListener('touchstart', function() { if (!isWalking && !subCompassWrapper.classList.contains(
                    'active')) { moveMainNeedle(angle);
                    statusValue.textContent = title } }, { passive: true });
            dir.addEventListener('click', function(e) {
                e.preventDefault();
                if (!isWalking && !subCompassWrapper.classList.contains('active')) { goToPage(pageKey) }
            })
        });
        homeLogo.addEventListener('click', function() { if (subCompassWrapper.classList.contains('active')) { goHome() } });
        homeCenter.addEventListener('click', function() { if (subCompassWrapper.classList.contains('active')) { goHome() } });
        backButton.addEventListener('click', function() { if (subCompassWrapper.classList.contains('active')) { goHome() } });
        document.addEventListener('keydown', function(e) { if (e.key === 'Escape') { if (subCompassWrapper.classList.contains(
                    'active')) { goHome() } } });
        moveMainNeedle(0);
        statusValue.textContent = 'Coaching';
    </script>
</body>
</html>
