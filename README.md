<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>偷偷戀愛中 - 偶像遊戲</title>
    <style>
        :root {
            --bg: #1a1a2e;
            --phone-bg: #f5f5f7;
            --accent: #ff6b9d;
            --accent2: #ff9a76;
            --text: #2d2d2d;
            --border: #e0e0e0;
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            --phone-width: 380px;
            --phone-height: 780px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 40%, #0f3460 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            font-family: 'Noto Sans TC', 'PingFang TC', 'Microsoft JhengHei', 'Segoe UI', sans-serif;
            padding: 20px;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        /* 手機外框 */
        .phone-container {
            position: relative;
            width: var(--phone-width);
            height: var(--phone-height);
            background: #1c1c1e;
            border-radius: 40px;
            padding: 12px;
            box-shadow:
                0 0 0 2px #2a2a2c,
                0 0 0 6px #1c1c1e,
                0 0 0 8px #2a2a2c,
                var(--shadow),
                0 20px 60px rgba(0, 0, 0, 0.5);
        }
        .phone-notch {
            position: absolute;
            top: 12px;
            left: 50%;
            transform: translateX(-50%);
            width: 120px;
            height: 28px;
            background: #1c1c1e;
            border-radius: 0 0 20px 20px;
            z-index: 10;
        }
        .phone-notch-inner {
            position: absolute;
            top: 6px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 5px;
            background: #2a2a2c;
            border-radius: 10px;
        }
        .phone-screen {
            width: 100%;
            height: 100%;
            background: var(--phone-bg);
            border-radius: 30px;
            overflow: hidden;
            position: relative;
            display: flex;
            flex-direction: column;
        }

        /* 狀態欄 */
        .status-bar {
            background: transparent;
            padding: 14px 20px 6px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 12px;
            font-weight: 600;
            color: #1c1c1e;
            z-index: 5;
            letter-spacing: 0.5px;
        }
        .status-bar .time {
            flex: 1;
        }
        .status-bar .icons {
            display: flex;
            gap: 7px;
            align-items: center;
        }
        .status-bar .icons span {
            font-size: 11px;
        }
        .signal-bars {
            display: flex;
            gap: 1.5px;
            align-items: flex-end;
            height: 12px;
        }
        .signal-bars .bar {
            width: 2.5px;
            background: #1c1c1e;
            border-radius: 1px;
        }
        .signal-bars .bar:nth-child(1) {
            height: 4px;
        }
        .signal-bars .bar:nth-child(2) {
            height: 6px;
        }
        .signal-bars .bar:nth-child(3) {
            height: 8px;
        }
        .signal-bars .bar:nth-child(4) {
            height: 11px;
        }
        .battery {
            width: 22px;
            height: 11px;
            border: 1.5px solid #1c1c1e;
            border-radius: 3px;
            position: relative;
            padding: 1.5px;
        }
        .battery::after {
            content: '';
            position: absolute;
            right: -3.5px;
            top: 50%;
            transform: translateY(-50%);
            width: 2.5px;
            height: 5px;
            background: #1c1c1e;
            border-radius: 0 2px 2px 0;
        }
        .battery-fill {
            height: 100%;
            background: #1c1c1e;
            border-radius: 1px;
            width: 75%;
        }

        /* 主畫面 */
        .main-screen {
            flex: 1;
            display: flex;
            flex-direction: column;
            padding: 8px 10px 10px 10px;
            overflow: hidden;
        }

        /* 應用程式網格 */
        .app-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            grid-template-rows: repeat(4, 1fr);
            gap: 10px 6px;
            padding: 10px 8px;
            flex: 1;
            align-content: center;
        }
        .app-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: transform 0.15s ease;
            gap: 5px;
        }
        .app-item:active {
            transform: scale(0.88);
        }
        .app-icon {
            width: 54px;
            height: 54px;
            border-radius: 13px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 28px;
            position: relative;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.12);
            transition: all 0.2s ease;
        }
        .app-icon.camera-icon {
            background: linear-gradient(135deg, #ff6b9d, #ff3d7f);
        }
        .app-icon.album-icon {
            background: linear-gradient(135deg, #ff9a76, #ffb347);
        }
        .app-icon.other-icon {
            background: linear-gradient(135deg, #e8e8ea, #d5d5d8);
        }
        .app-label {
            font-size: 10px;
            color: #555;
            text-align: center;
            font-weight: 500;
            letter-spacing: 0.3px;
        }

        /* 設定頁面 */
        .setup-overlay {
            position: absolute;
            inset: 0;
            background: #fefefe;
            z-index: 20;
            border-radius: 30px;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
            padding: 16px 18px;
        }
        .setup-overlay h2 {
            text-align: center;
            font-size: 20px;
            color: #333;
            margin-bottom: 6px;
            letter-spacing: 1px;
        }
        .setup-overlay .subtitle {
            text-align: center;
            font-size: 11px;
            color: #999;
            margin-bottom: 14px;
            letter-spacing: 0.5px;
        }
        .setup-section {
            margin-bottom: 14px;
            background: #fafafa;
            border-radius: 14px;
            padding: 12px 14px;
            border: 1px solid #eee;
        }
        .setup-section h3 {
            font-size: 13px;
            color: #555;
            margin-bottom: 8px;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .setup-section h3 .dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            display: inline-block;
        }
        .dot.self {
            background: #ff6b9d;
        }
        .dot.idol {
            background: #ff9a76;
        }
        .avatar-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            align-items: center;
        }
        .avatar-option {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            cursor: pointer;
            border: 3px solid transparent;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 26px;
            background: #fff;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
            position: relative;
        }
        .avatar-option:hover {
            transform: scale(1.1);
        }
        .avatar-option.selected {
            border-color: #ff6b9d;
            box-shadow: 0 0 0 4px rgba(255, 107, 157, 0.2);
        }
        .avatar-option.idol-selected {
            border-color: #ff9a76;
            box-shadow: 0 0 0 4px rgba(255, 154, 118, 0.2);
        }
        .avatar-upload {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            cursor: pointer;
            border: 3px dashed #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            background: #fff;
            transition: all 0.2s ease;
            color: #aaa;
            position: relative;
        }
        .avatar-upload:hover {
            border-color: #ff6b9d;
            color: #ff6b9d;
        }
        .setup-input {
            width: 100%;
            padding: 10px 12px;
            border: 1.5px solid #e0e0e0;
            border-radius: 10px;
            font-size: 14px;
            outline: none;
            transition: border 0.2s;
            font-family: inherit;
            background: #fff;
        }
        .setup-input:focus {
            border-color: #ff6b9d;
        }
        .gender-options {
            display: flex;
            gap: 8px;
        }
        .gender-btn {
            flex: 1;
            padding: 9px;
            border: 1.5px solid #e0e0e0;
            border-radius: 10px;
            cursor: pointer;
            text-align: center;
            font-size: 13px;
            background: #fff;
            transition: all 0.2s;
            font-family: inherit;
        }
        .gender-btn:hover {
            border-color: #ff6b9d;
        }
        .gender-btn.selected-gender {
            background: #ff6b9d;
            color: #fff;
            border-color: #ff6b9d;
        }
        .start-btn {
            display: block;
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, #ff6b9d, #ff3d7f);
            color: #fff;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            cursor: pointer;
            font-weight: 700;
            letter-spacing: 2px;
            transition: all 0.3s;
            box-shadow: 0 6px 20px rgba(255, 61, 127, 0.35);
            font-family: inherit;
            margin-top: 4px;
        }
        .start-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 28px rgba(255, 61, 127, 0.45);
        }
        .start-btn:active {
            transform: scale(0.96);
        }

        /* 相機畫面 */
        .camera-view {
            position: absolute;
            inset: 0;
            background: #000;
            z-index: 15;
            border-radius: 30px;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .camera-view.hidden {
            display: none;
        }
        .camera-preview {
            flex: 1;
            background: #1a1a1a;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }
        .camera-preview canvas {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }
        .camera-preview .placeholder-text {
            color: #555;
            font-size: 14px;
            letter-spacing: 1px;
        }
        .camera-controls {
            padding: 16px 20px;
            display: flex;
            align-items: center;
            justify-content: space-around;
            background: #111;
            gap: 10px;
        }
        .flash-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #333;
            color: #fff;
            border: none;
            cursor: pointer;
            font-size: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }
        .flash-btn.active {
            background: #ffcc00;
            color: #000;
        }
        .shutter-btn {
            width: 64px;
            height: 64px;
            border-radius: 50%;
            background: #fff;
            border: 5px solid #ddd;
            cursor: pointer;
            transition: all 0.15s;
            position: relative;
        }
        .shutter-btn:active {
            transform: scale(0.9);
            border-color: #ff6b9d;
        }
        .shutter-btn-inner {
            width: 44px;
            height: 44px;
            border-radius: 50%;
            background: #fff;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        .close-camera {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #333;
            color: #fff;
            border: none;
            cursor: pointer;
            font-size: 18px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }
        .mini-album {
            width: 40px;
            height: 40px;
            border-radius: 8px;
            background: #444;
            cursor: pointer;
            overflow: hidden;
            border: 2px solid #555;
            transition: all 0.2s;
            flex-shrink: 0;
        }
        .mini-album img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        .shutter-options {
            position: absolute;
            bottom: 130px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(30, 30, 30, 0.95);
            border-radius: 16px;
            padding: 10px 14px;
            display: flex;
            gap: 12px;
            z-index: 20;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
        }
        .shutter-options.hidden {
            display: none;
        }
        .shutter-option {
            padding: 10px 16px;
            border-radius: 20px;
            cursor: pointer;
            color: #fff;
            font-size: 13px;
            font-weight: 600;
            letter-spacing: 0.5px;
            transition: all 0.2s;
            white-space: nowrap;
            border: none;
            font-family: inherit;
        }
        .shutter-option.selfie {
            background: #ff6b9d;
        }
        .shutter-option.scenery {
            background: #4ecb71;
        }
        .shutter-option.food {
            background: #ff9a76;
        }
        .scene-input-overlay {
            position: absolute;
            bottom: 130px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(30, 30, 30, 0.95);
            border-radius: 16px;
            padding: 14px;
            z-index: 21;
            display: flex;
            gap: 8px;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
            align-items: center;
        }
        .scene-input-overlay.hidden {
            display: none;
        }
        .scene-input-overlay input {
            padding: 10px 14px;
            border-radius: 20px;
            border: none;
            font-size: 13px;
            width: 160px;
            outline: none;
            font-family: inherit;
        }
        .scene-input-overlay button {
            padding: 10px 16px;
            border-radius: 20px;
            border: none;
            cursor: pointer;
            font-weight: 600;
            font-size: 13px;
            background: #ff6b9d;
            color: #fff;
            font-family: inherit;
        }

        /* 相簿檢視（放大照片） */
        .photo-viewer {
            position: absolute;
            inset: 0;
            background: rgba(0, 0, 0, 0.92);
            z-index: 25;
            border-radius: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .photo-viewer.hidden {
            display: none;
        }
        .photo-viewer img {
            max-width: 90%;
            max-height: 55%;
            border-radius: 10px;
            cursor: pointer;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
        }
        .photo-viewer .edit-textbox {
            position: absolute;
            border: 2px dashed #ff6b9d;
            border-radius: 6px;
            min-width: 60px;
            min-height: 30px;
            padding: 6px 10px;
            cursor: move;
            color: #fff;
            font-size: 14px;
            background: rgba(0, 0, 0, 0.5);
            outline: none;
            z-index: 5;
            display: none;
            white-space: nowrap;
        }
        .photo-viewer .edit-textbox.active {
            display: block;
        }
        .photo-viewer-toolbar {
            display: flex;
            gap: 16px;
            margin-top: 16px;
            flex-wrap: wrap;
            justify-content: center;
        }
        .photo-tool-btn {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            color: #fff;
            font-size: 11px;
            transition: all 0.2s;
            background: none;
            border: none;
            font-family: inherit;
        }
        .photo-tool-btn .tool-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            transition: all 0.2s;
        }
        .photo-tool-btn.delete .tool-icon {
            background: #e74c3c;
        }
        .photo-tool-btn.edit .tool-icon {
            background: #3498db;
        }
        .photo-tool-btn.more .tool-icon {
            background: #666;
        }
        .photo-tool-btn.share .tool-icon {
            background: #2ecc71;
        }
        .more-options-popup {
            position: absolute;
            bottom: 100px;
            background: #2a2a2a;
            border-radius: 14px;
            padding: 8px 0;
            z-index: 30;
            display: flex;
            flex-direction: column;
            box-shadow: 0 8px 24px rgba(0, 0, 0, 0.6);
        }
        .more-options-popup.hidden {
            display: none;
        }
        .more-option-item {
            padding: 12px 18px;
            color: #fff;
            cursor: pointer;
            font-size: 13px;
            white-space: nowrap;
            transition: background 0.2s;
            border: none;
            background: none;
            text-align: left;
            font-family: inherit;
            letter-spacing: 0.5px;
        }
        .more-option-item:hover {
            background: #444;
        }
        .confirm-dialog {
            position: absolute;
            inset: 0;
            background: rgba(0, 0, 0, 0.7);
            z-index: 35;
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .confirm-dialog.hidden {
            display: none;
        }
        .confirm-dialog-box {
            background: #fff;
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            max-width: 280px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        .confirm-dialog-box p {
            margin-bottom: 14px;
            font-size: 14px;
            color: #333;
        }
        .confirm-dialog-box button {
            padding: 10px 20px;
  
