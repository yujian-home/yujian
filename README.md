[index.html](https://github.com/user-attachments/files/24272329/index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>屿间导航</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- 添加字体库 -->
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Pacifico&family=Playfair+Display:wght@700&family=Roboto:wght@400;700&family=Montserrat:wght@700&family=ZCOOL+QingKe+HuangYou&family=Ma+Shan+Zheng&family=Liu+Jian+Mao+Cao&family=Noto+Sans+SC:wght@300;400;500&family=Long+Cang&family=ZCOOL+XiaoWei&family=Caveat:wght@700&family=Shadows+Into+Light&family=Fredericka+the+Great&family=Special+Elite&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #667eea;
            --secondary-color: #764ba2;
            --bg-color: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --text-color: #ffffff;
            --shadow-color: rgba(0, 0, 0, 0.2);
            --category-color: #ffffff;
            --bookmark-color: #ffffff;
            --title-font: "Pacifico", cursive;
            --subtitle-font: "'Long Cang', cursive";
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }

        body {
            background: var(--bg-color);
            color: var(--text-color);
            min-height: 100vh;
            transition: background 0.5s ease, color 0.5s ease;
            padding: 20px;
            position: relative;
            padding-bottom: 100px;
        }

        /* 增强磨砂质感 */
        .texture-layer {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)' opacity='0.2'/%3E%3C/svg%3E");
            z-index: 0;
            pointer-events: none;
            opacity: 0.5;
        }

        body.no-texture .texture-layer {
            display: none;
        }

        .background-image {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            z-index: -1;
            opacity: 1;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
            padding-top: 10%;
            padding-left: 0;
            padding-right: 0;
        }

        /* 标题样式 */
        .header {
            text-align: center;
            padding: 10px 0 20px;
            position: relative;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 130px;
            margin-bottom: 10px;
        }

        .page-title-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
            margin-bottom: 10px;
        }

        .page-title {
            font-size: 3.2rem;
            margin-bottom: 5px;
            text-shadow: 2px 2px 4px var(--shadow-color);
            font-weight: 700;
            padding: 10px 20px;
            border-radius: 12px;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            color: var(--text-color);
            font-family: var(--title-font);
            line-height: 1.2;
        }

        .page-title:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        .page-subtitle {
            font-size: 1.3rem;
            color: rgba(255, 255, 255, 0.85);
            font-family: var(--subtitle-font);
            font-weight: 300;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
            max-width: 600px;
            line-height: 1.5;
            margin-top: 5px;
        }

        .page-title-icon {
            width: 60px;
            height: 60px;
            margin-right: 15px;
            vertical-align: middle;
            border-radius: 10px;
            object-fit: cover;
            display: inline-block;
            transition: all 0.3s ease;
        }

        .page-title-icon.empty {
            display: none;
        }

        /* 标题编辑按钮 */
        .title-edit-buttons {
            position: absolute;
            top: -15px;
            right: -15px;
            display: none;
            gap: 5px;
            z-index: 10;
        }

        .edit-mode .title-edit-buttons {
            display: none !important;
        }

        .edit-btn-small {
            background: rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.4);
            border-radius: 50%;
            width: 22px;
            height: 22px;
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 10px;
            transition: all 0.2s;
        }

        .edit-btn-small:hover {
            background: rgba(255, 255, 255, 0.35);
            transform: scale(1.1);
        }

        /* 搜索框样式 - 左对齐，与网址栏对齐 */
        .search-container {
            max-width: 1400px;
            margin: 0 auto 25px;
            position: relative;
            z-index: 10;
            padding-left: 0;
            padding-right: 0;
        }

        .search-box {
            display: flex;
            align-items: center;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border-radius: 50px;
            padding: 5px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            width: 100%;
        }

        .search-engine-selector {
            position: relative;
            min-width: 60px;
            z-index: 100;
        }

        .current-engine {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0;
            padding: 12px 15px;
            cursor: pointer;
            border-radius: 50px;
            transition: all 0.3s;
            font-weight: 500;
            width: 60px;
        }

        .current-engine:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        /* 修复百度图标 - 确保正确显示 */
        .current-engine .fa-baidu {
            color: #2932e1 !important;
            filter: none !important;
            font-size: 24px;
            line-height: 24px;
        }

        .current-engine:hover .fa-baidu {
            color: #2932e1 !important;
            filter: none !important;
        }

        .engine-grid.show .fa-baidu {
            color: #2932e1 !important;
            filter: none !important;
            font-size: 22px;
            line-height: 22px;
        }

        /* 搜索引擎网格样式 */
        .engine-grid {
            position: absolute;
            top: 100%;
            left: 0;
            width: 400px;
            background: rgba(255, 255, 255, 0.98);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            margin-top: 8px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.25);
            display: none;
            z-index: 1000;
            color: #333;
            padding: 15px;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        .engine-grid.show {
            display: grid;
        }

        .engine-grid-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 12px 8px;
            cursor: pointer;
            transition: all 0.2s;
            border-radius: 8px;
            text-align: center;
            min-height: 70px;
        }

        .engine-grid-item:hover {
            background: rgba(102, 126, 234, 0.1);
            transform: translateY(-2px);
        }

        .engine-grid-icon {
            font-size: 22px;
            margin-bottom: 5px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .engine-grid-name {
            font-size: 12px;
            line-height: 1.3;
        }

        .search-input {
            flex: 1;
            padding: 12px 15px;
            border: none;
            background: transparent;
            color: white;
            font-size: 16px;
            outline: none;
        }

        .search-input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }

        .search-input.disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .search-btn {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 50%;
            width: 46px;
            height: 46px;
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            margin-right: 3px;
        }

        .search-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: scale(1.05);
        }

        .search-btn.disabled {
            opacity: 0.5;
            cursor: not-allowed;
            pointer-events: none;
        }

        /* 分类按钮样式 - 恢复居中 */
        .categories-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center; /* 改为居中 */
            gap: 8px;
            margin-bottom: 25px;
            position: relative;
            min-height: 40px;
            padding-left: 0;
            width: 100%;
        }

        .category-item {
            position: relative;
            cursor: move;
        }

        .category-item.dragging {
            opacity: 0.5;
            transform: scale(1.05);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            z-index: 100;
        }

        .category-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid rgba(255, 255, 255, 0.3);
            color: var(--category-color);
            padding: 6px 15px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            font-weight: 500;
            position: relative;
            display: inline-block;
        }

        .category-btn.active,
        .category-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            border-color: rgba(255, 255, 255, 0.6);
        }

        .category-btn.active {
            color: var(--category-color);
            border-color: rgba(255, 255, 255, 0.8);
        }

        /* 添加分类按钮 */
        .add-category-btn {
            background: rgba(255, 255, 255, 0.05);
            border: 2px dashed rgba(255, 255, 255, 0.3);
            color: rgba(255, 255, 255, 0.7);
            padding: 6px 12px;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            display: none;
        }

        .edit-mode .add-category-btn {
            display: inline-block;
        }

        .add-category-btn:hover {
            background: rgba(255, 255, 255, 0.1);
            color: white;
            border-color: rgba(255, 255, 255, 0.5);
        }

        /* 分类编辑按钮 */
        .category-edit-buttons {
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            display: none;
            gap: 5px;
            z-index: 10;
        }

        .edit-mode .category-edit-buttons {
            display: flex;
        }

        /* 网站网格样式 */
        .bookmarks-section {
            display: none;
            animation: fadeIn 0.5s;
        }

        .bookmarks-section.active {
            display: block;
        }

        /* 增加行与行之间的间距 */
        .bookmarks-grid {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 12px; /* 增大间距 */
            margin-top: 15px;
        }

        .edit-mode .bookmarks-grid {
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 10px;
            background: rgba(255, 255, 255, 0.03);
        }

        .bookmark-item {
            transition: all 0.3s;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: flex-start;
            gap: 8px;
            cursor: pointer;
            border: none;
            background: transparent;
            color: var(--bookmark-color);
            min-height: 48px; /* 稍微增加高度 */
            padding: 8px 10px;
            border-radius: 8px;
            text-decoration: none;
            width: 170px;
            overflow: hidden;
        }

        .bookmark-item.dragging {
            opacity: 0.5;
            transform: scale(1.05) rotate(5deg);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            border: 2px dashed rgba(255, 255, 255, 0.5);
            z-index: 100;
        }

        .bookmark-item:hover {
            background: rgba(255, 255, 255, 0.08);
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
        }

        .empty-slot {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }

        .edit-mode .empty-slot {
            opacity: 0.3;
            visibility: visible;
            pointer-events: auto;
        }

        .bookmark-icon {
            width: 28px; /* 稍微增大图标 */
            height: 28px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .bookmark-icon-img {
            width: 26px; /* 稍微增大图片图标 */
            height: 26px;
            object-fit: contain;
        }

        /* 增大网站按钮字体 */
        .bookmark-name {
            font-size: 18px; /* 增大字体 */
            flex: 1;
            text-align: left;
            word-break: break-all;
            line-height: 1.2;
            font-weight: 500;
            overflow: hidden;
            max-height: 40px;
            min-height: 20px;
            display: -webkit-box;
            -webkit-line-clamp: 1;
            -webkit-box-orient: vertical;
            white-space: nowrap;
            text-overflow: ellipsis;
            max-width: 100px;
        }

        .bookmark-edit-btn {
            position: absolute;
            top: 5px;
            right: 5px;
            background: rgba(255, 255, 255, 0.25);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.4);
            border-radius: 50%;
            width: 20px;
            height: 20px;
            color: white;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            font-size: 10px;
            transition: all 0.2s;
            z-index: 5;
        }

        .edit-mode .bookmark-edit-btn {
            display: flex;
        }

        .bookmark-edit-btn:hover {
            background: rgba(255, 255, 255, 0.35);
            transform: scale(1.1);
        }

        /* 添加行按钮 */
        .add-row-btn {
            grid-column: 1 / -1;
            background: rgba(255, 255, 255, 0.05);
            border: 1px dashed rgba(255, 255, 255, 0.2);
            color: rgba(255, 255, 255, 0.5);
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            display: none;
            justify-content: center;
            align-items: center;
            gap: 6px;
            font-size: 14px;
            margin-top: 10px;
        }

        .edit-mode .add-row-btn {
            display: flex;
        }

        .add-row-btn:hover {
            background: rgba(255, 255, 255, 0.1);
            color: rgba(255, 255, 255, 0.8);
            border-color: rgba(255, 255, 255, 0.3);
        }

        /* 删除行按钮 */
        .remove-row-btn {
            grid-column: 1 / -1;
            background: rgba(255, 107, 107, 0.1);
            border: 1px dashed rgba(255, 107, 107, 0.3);
            color: rgba(255, 107, 107, 0.7);
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            display: none;
            justify-content: center;
            align-items: center;
            gap: 6px;
            font-size: 14px;
            margin-top: 6px;
        }

        .edit-mode .remove-row-btn {
            display: flex;
        }

        .remove-row-btn:hover {
            background: rgba(255, 107, 107, 0.2);
            color: rgba(255, 107, 107, 0.9);
            border-color: rgba(255, 107, 107, 0.5);
        }

        /* 右下角设置按钮 */
        .settings-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            font-size: 20px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
            z-index: 100;
        }

        .settings-btn:hover {
            background: rgba(255, 255, 255, 0.25);
            transform: scale(1.1) rotate(30deg);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
        }

        .settings-btn.confirm-mode {
            background: rgba(76, 175, 80, 0.8) !important;
            border-color: rgba(76, 175, 80, 0.9) !important;
        }

        .settings-btn.confirm-mode:hover {
            background: rgba(76, 175, 80, 0.9) !important;
        }

        /* 设置菜单 */
        .settings-menu {
            position: fixed;
            bottom: 90px;
            right: 30px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 15px;
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.2);
            display: none;
            flex-direction: column;
            gap: 10px;
            min-width: 200px;
            z-index: 100;
            color: #333;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .settings-menu.show {
            display: flex;
        }

        .settings-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px 15px;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.2s;
            font-size: 14px;
            color: #333;
            text-decoration: none;
            border: none;
            background: transparent;
            width: 100%;
            text-align: left;
        }

        .settings-item:hover {
            background: rgba(102, 126, 234, 0.1);
        }

        /* 配色和背景模态框 - 加宽 */
        .color-bg-modal-content {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 15px;
            padding: 30px;
            width: 95%;
            max-width: 800px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            color: #333;
            max-height: 85vh;
            overflow-y: auto;
        }

        .color-tabs {
            display: flex;
            gap: 5px;
            margin-bottom: 20px;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }

        .color-tab {
            padding: 8px 16px;
            border: none;
            background: #f5f5f5;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.2s;
        }

        .color-tab.active {
            background: var(--primary-color);
            color: white;
        }

        .color-tab:hover:not(.active) {
            background: #e0e0e0;
        }

        .color-tab-content {
            display: none;
        }

        .color-tab-content.active {
            display: block;
        }

        /* 皮肤网格 */
        .skin-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-top: 15px;
        }

        .skin-item {
            background: #f5f5f5;
            border-radius: 12px;
            overflow: hidden;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
        }

        .skin-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
        }

        .skin-item.selected {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 2px rgba(102, 126, 234, 0.3);
        }

        .skin-preview {
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 16px;
        }

        .skin-name {
            padding: 10px;
            text-align: center;
            background: white;
            font-size: 14px;
            font-weight: 500;
        }

        /* 颜色选择器 */
        .color-picker-container {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 15px;
        }

        .color-label {
            min-width: 100px;
            font-weight: 500;
        }

        .custom-color-input {
            width: 40px;
            height: 40px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            padding: 0;
            overflow: hidden;
        }

        .custom-color-input::-webkit-color-swatch-wrapper {
            padding: 0;
        }

        .custom-color-input::-webkit-color-swatch {
            border: none;
        }

        .color-value {
            font-size: 14px;
            color: #666;
            min-width: 70px;
        }

        /* 壁纸选项 */
        .bg-options {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin-top: 15px;
        }

        .bg-option {
            height: 80px;
            border-radius: 8px;
            cursor: pointer;
            border: 2px solid transparent;
            transition: all 0.2s;
            overflow: hidden;
            position: relative;
        }

        .bg-option:hover {
            transform: scale(1.05);
        }

        .bg-option.selected {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.8);
        }

        .bg-option-text {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
        }

        /* 模态框样式 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 2000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 15px;
            padding: 30px;
            width: 90%;
            max-width: 500px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            color: #333;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-title {
            font-size: 1.5rem;
            font-weight: 600;
            color: #333;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #444;
        }

        .form-input {
            width: 100%;
            padding: 12px 15px;
            border-radius: 8px;
            border: 1px solid #ddd;
            font-size: 1rem;
            transition: border 0.3s;
        }

        .form-input:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 2px rgba(102, 126, 234, 0.2);
        }

        .form-actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            margin-top: 25px;
        }

        .btn {
            padding: 10px 20px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
        }

        .btn-primary {
            background: var(--primary-color);
            color: white;
        }

        .btn-primary:hover {
            background: #5a6fd8;
        }

        .btn-secondary {
            background: #f0f0f0;
            color: #333;
        }

        .btn-secondary:hover {
            background: #e0e0e0;
        }

        /* 新增：数据文本域样式 */
        .data-textarea {
            width: 100%;
            height: 200px;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #ddd;
            font-family: monospace;
            font-size: 14px;
            resize: vertical;
            margin-bottom: 15px;
        }

        .data-textarea:focus {
            outline: none;
            border-color: var(--primary-color);
        }

        /* 错误提示样式 */
        .error-message {
            color: #ff6b6b;
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }

        .error-message.show {
            display: block;
        }

        /* 图标选择器样式 */
        .icon-selector {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 10px;
            margin-top: 10px;
            max-height: 200px;
            overflow-y: auto;
            padding: 10px;
        }

        .icon-option {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 20px;
            color: white;
            background: rgba(0, 0, 0, 0.1);
        }

        .icon-option:hover {
            background: rgba(102, 126, 234, 0.8);
            transform: scale(1.1);
        }

        .icon-option.selected {
            background: var(--primary-color);
            color: white;
            transform: scale(1.1);
            box-shadow: 0 0 10px rgba(102, 126, 234, 0.5);
        }

        /* 拖拽提示 */
        .drag-hint {
            color: rgba(255, 255, 255, 0.7);
            text-align: center;
            font-size: 14px;
            margin-top: 10px;
            display: none;
        }

        .edit-mode .drag-hint {
            display: block;
        }

        /* 字体选择器样式 - 加宽布局 */
        .font-selector {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-top: 10px;
            max-height: 200px;
            overflow-y: auto;
            padding: 12px;
        }

        .font-option {
            padding: 12px 8px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 16px;
            text-align: center;
            background: rgba(0, 0, 0, 0.05);
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: inherit;
        }

        .font-option:hover {
            background: rgba(102, 126, 234, 0.2);
            transform: scale(1.05);
        }

        .font-option.selected {
            background: var(--primary-color);
            color: white;
            transform: scale(1.05);
            box-shadow: 0 0 10px rgba(102, 126, 234, 0.5);
        }

        /* 标题图标预览 */
        .title-icon-preview {
            width: 60px;
            height: 60px;
            border-radius: 10px;
            object-fit: cover;
            margin: 10px auto;
            display: block;
            border: 2px solid #ddd;
        }

        /* 隐藏页切换按钮 */
        .page-switcher {
            position: fixed;
            top: 50%;
            transform: translateY(-50%);
            width: 40px;
            height: 100px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            transition: all 0.3s;
            z-index: 90;
            opacity: 0;
        }

        .page-switcher:hover {
            opacity: 1;
            background: rgba(255, 255, 255, 0.25);
            width: 50px;
        }

        .page-switcher-left {
            left: 0;
            border-radius: 0 10px 10px 0;
        }

        .page-switcher-right {
            right: 0;
            border-radius: 10px 0 0 10px;
        }

        /* 当前页面指示器 - 隐藏 */
        .page-indicator {
            display: none !important;
        }

        /* 网站分类图标颜色 */
        .icon-search { color: #4285f4; }
        .icon-social { color: #e4405f; }
        .icon-shopping { color: #ff6b6b; }
        .icon-travel { color: #4ecdc4; }
        .icon-work { color: #45b7d1; }
        .icon-education { color: #96ceb4; }
        .icon-entertainment { color: #feca57; }
        .icon-news { color: #ff9f43; }
        .icon-tools { color: #54a0ff; }
        .icon-music { color: #5f27cd; }
        .icon-video { color: #ee5a24; }
        .icon-games { color: #00d2d3; }
        .icon-food { color: #ff9ff3; }
        .icon-health { color: #1dd1a1; }
        .icon-finance { color: #f368e0; }
        .icon-tech { color: #0abde3; }
        .icon-sports { color: #10ac84; }
        .icon-weather { color: #48dbfb; }
        .icon-books { color: #ff9a76; }
        .icon-art { color: #d63031; }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes dragPulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .dragging-pulse {
            animation: dragPulse 1s infinite;
        }

        /* 新增：管理行数确认对话框 */
        .confirm-dialog {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 15px;
            padding: 25px;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            color: #333;
            text-align: center;
        }

        .confirm-title {
            font-size: 1.2rem;
            font-weight: 600;
            margin-bottom: 15px;
            color: #333;
        }

        .confirm-message {
            font-size: 1rem;
            margin-bottom: 20px;
            color: #666;
        }

        .confirm-actions {
            display: flex;
            gap: 10px;
            justify-content: center;
        }

        /* 手机端优化 - 搜索框 */
        @media (max-width: 768px) {
            .search-box {
                flex-direction: row;
                border-radius: 15px;
                padding: 5px;
                flex-wrap: nowrap;
            }
            
            .search-engine-selector {
                width: auto;
                margin-bottom: 0;
                min-width: 60px;
            }
            
            .search-input {
                width: auto;
                margin-bottom: 0;
                flex: 1;
                font-size: 14px;
            }
            
            /* 手机端隐藏搜索框占位符文字 */
            .search-input::placeholder {
                color: transparent;
            }
            
            .search-input::-webkit-input-placeholder {
                color: transparent;
            }
            
            .search-input::-moz-placeholder {
                color: transparent;
            }
            
            .search-input:-ms-input-placeholder {
                color: transparent;
            }
            
            .search-input:focus::placeholder {
                color: transparent;
            }
            
            .search-btn {
                width: 40px;
                height: 40px;
                margin-right: 0;
            }
            
            .current-engine {
                width: 50px;
                padding: 8px 10px;
            }
            
            .engine-grid {
                width: 250px;
                grid-template-columns: repeat(2, 1fr);
                left: 50%;
                transform: translateX(-50%);
            }
            
            .bookmarks-grid {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .categories-container {
                gap: 8px;
            }
            
            .category-btn {
                padding: 6px 15px;
                font-size: 14px;
            }
        }

        @media (max-width: 1200px) {
            .bookmarks-grid {
                grid-template-columns: repeat(5, 1fr);
            }
            
            .engine-grid {
                width: 350px;
                grid-template-columns: repeat(3, 1fr);
            }
            
            .icon-selector {
                grid-template-columns: repeat(5, 1fr);
            }
            
            .skin-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 992px) {
            .bookmarks-grid {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .page-title {
                font-size: 2.5rem;
            }
            
            .engine-grid {
                width: 300px;
                grid-template-columns: repeat(3, 1fr);
            }
            
            .icon-selector {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .skin-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .bg-options {
                grid-template-columns: repeat(3, 1fr);
            }
        }

        @media (max-width: 768px) {
            .bookmarks-grid {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .settings-menu {
                right: 15px;
                bottom: 80px;
            }
            
            .icon-selector {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .skin-grid {
                grid-template-columns: repeat(1, 1fr);
            }
            
            .bg-options {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 576px) {
            .bookmarks-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .page-title {
                font-size: 2rem;
            }
            
            .page-subtitle {
                font-size: 0.9rem;
                padding: 0 15px;
            }
            
            .engine-grid {
                width: 200px;
                grid-template-columns: repeat(2, 1fr);
            }
            
            .icon-selector {
                grid-template-columns: repeat(3, 1fr);
            }
            
            .skin-grid {
                grid-template-columns: repeat(1, 1fr);
            }
            
            .bg-options {
                grid-template-columns: repeat(2, 1fr);
            }
            
            /* 手机端进一步优化 */
            .search-box {
                padding: 3px;
            }
            
            .search-input {
                font-size: 12px;
                padding: 8px 10px;
            }
            
            .current-engine {
                width: 45px;
                padding: 6px 8px;
            }
            
            .search-engine-selector {
                min-width: 45px;
            }
            
            .engine-grid {
                width: 180px;
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <!-- 纹理层 -->
    <div class="texture-layer"></div>
    
    <!-- 背景图片 -->
    <img class="background-image" id="backgroundImage" src="" alt="背景">
    
    <!-- 页面指示器 -->
    <div class="page-indicator" id="pageIndicator">页面 1</div>
    
    <!-- 隐藏页切换按钮 -->
    <div class="page-switcher page-switcher-right" id="pageSwitcherRight">
        <i class="fas fa-chevron-right"></i>
    </div>
    
    <div class="container" id="mainContainer">
        <!-- 标题 -->
        <div class="header">
            <div class="page-title-container">
                <div class="title-edit-buttons">
                    <button class="edit-btn-small rename-title-btn">
                        <i class="fas fa-edit"></i>
                    </button>
                    <button class="edit-btn-small delete-title-btn">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
                <h1 class="page-title" id="pageTitle">屿间</h1>
            </div>
            <div class="page-subtitle" id="pageSubtitle">
                每一次与过往照面，都是为了与未来更好地相逢。
            </div>
        </div>
        
        <!-- 搜索框 -->
        <div class="search-container">
            <div class="search-box">
                <div class="search-engine-selector">
                    <div class="current-engine" id="currentEngine">
                        <i class="fab fa-google"></i>
                        <span class="engine-name" style="display: none;">谷歌</span>
                    </div>
                    <div class="engine-grid" id="engineGrid">
                        <!-- 搜索引擎将通过JS动态生成 -->
                    </div>
                </div>
                <input type="text" class="search-input" id="searchInput" placeholder="输入搜索内容或网址...">
                <button class="search-btn" id="searchBtn">
                    <i class="fas fa-search"></i>
                </button>
            </div>
        </div>
        
        <!-- 分类标签 -->
        <div class="categories-container" id="categoriesContainer">
            <!-- 分类按钮将通过JS动态生成 -->
        </div>
        
        <!-- 拖拽提示 -->
        <div class="drag-hint" id="dragHint">
            <i class="fas fa-arrows-alt"></i> 拖拽分类或网站可以调整顺序
        </div>
        
        <!-- 网站内容区域 -->
        <div id="bookmarksContainer">
            <!-- 网站将通过JS动态生成 -->
        </div>
    </div>
    
    <!-- 隐藏页内容 -->
    <div class="container" id="hiddenContainer" style="display: none;">
        <!-- 标题 -->
        <div class="header">
            <div class="page-title-container">
                <div class="title-edit-buttons">
                    <button class="edit-btn-small rename-title-btn">
                        <i class="fas fa-edit"></i>
                    </button>
                    <button class="edit-btn-small delete-title-btn">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
                <h1 class="page-title" id="hiddenPageTitle">屿间</h1>
            </div>
            <div class="page-subtitle" id="hiddenPageSubtitle">
                每一次与过往照面，都是为了与未来更好地相逢。
            </div>
        </div>
        
        <!-- 搜索框 -->
        <div class="search-container">
            <div class="search-box">
                <div class="search-engine-selector">
                    <div class="current-engine" id="hiddenCurrentEngine">
                        <i class="fab fa-google"></i>
                        <span class="engine-name" style="display: none;">谷歌</span>
                    </div>
                    <div class="engine-grid" id="hiddenEngineGrid">
                        <!-- 搜索引擎将通过JS动态生成 -->
                    </div>
                </div>
                <input type="text" class="search-input" id="hiddenSearchInput" placeholder="输入搜索内容或网址...">
                <button class="search-btn" id="hiddenSearchBtn">
                    <i class="fas fa-search"></i>
                </button>
            </div>
        </div>
        
        <!-- 分类标签 -->
        <div class="categories-container" id="hiddenCategoriesContainer">
            <!-- 分类按钮将通过JS动态生成 -->
        </div>
        
        <!-- 拖拽提示 -->
        <div class="drag-hint" id="hiddenDragHint">
            <i class="fas fa-arrows-alt"></i> 拖拽分类或网站可以调整顺序
        </div>
        
        <!-- 网站内容区域 -->
        <div id="hiddenBookmarksContainer">
            <!-- 网站将通过JS动态生成 -->
        </div>
    </div>
    
    <!-- 隐藏页切换按钮 -->
    <div class="page-switcher page-switcher-left" id="pageSwitcherLeft" style="display: none;">
        <i class="fas fa-chevron-left"></i>
    </div>
    
    <!-- 右下角设置按钮 -->
    <button class="settings-btn" id="settingsBtn">
        <i class="fas fa-cog"></i>
    </button>
    
    <!-- 设置菜单 -->
    <div class="settings-menu" id="settingsMenu">
        <button class="settings-item" id="customizeBtn">
            <i class="fas fa-sliders-h"></i> 自定义模式
        </button>
        <!-- 移除编辑标题按钮 -->
        <button class="settings-item" id="colorBgBtn">
            <i class="fas fa-palette"></i> 配色与背景
        </button>
        <!-- 移除管理行数按钮 -->
        <button class="settings-item" id="importExportBtn">
            <i class="fas fa-file-export"></i> 数据备份与恢复
        </button>
        <button class="settings-item" id="resetBtn">
            <i class="fas fa-redo"></i> 恢复默认
        </button>
    </div>
    
    <!-- 编辑网站模态框 -->
    <div class="modal" id="editBookmarkModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">编辑网站</h2>
                <button class="close-modal" id="closeEditModalBtn">&times;</button>
            </div>
            <form id="editBookmarkForm">
                <div class="form-group">
                    <label class="form-label" for="editBookmarkName">网站名称 (最多15个字符)</label>
                    <input type="text" class="form-input" id="editBookmarkName" required maxlength="15">
                    <small style="color: #666; display: block; margin-top: 5px;">提示：最多显示8个汉字长度，完整名称可在鼠标悬停时查看</small>
                </div>
                <div class="form-group">
                    <label class="form-label" for="editBookmarkUrl">网站地址 (URL)</label>
                    <input type="text" class="form-input" id="editBookmarkUrl" required placeholder="https://example.com">
                    <small style="color: #666; display: block; margin-top: 5px;">提示：请输入完整的URL地址，如 https://www.google.com</small>
                </div>
                <div class="form-group">
                    <label class="form-label">选择图标</label>
                    <div class="icon-selector" id="iconSelector">
                        <!-- 图标将通过JS动态生成 -->
                    </div>
                    <small style="color: #666; display: block; margin-top: 5px;">提示：选择网站图标，如无法获取网站图标将使用此图标</small>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelEditBtn">取消</button>
                    <button type="submit" class="btn btn-primary" id="saveEditBtn">保存</button>
                </div>
            </form>
        </div>
    </div>
    
    <!-- 编辑分类模态框 -->
    <div class="modal" id="editCategoryModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">编辑分类</h2>
                <button class="close-modal" id="closeCategoryModalBtn">&times;</button>
            </div>
            <form id="editCategoryForm">
                <div class="form-group">
                    <label class="form-label" for="editCategoryName">分类名称</label>
                    <input type="text" class="form-input" id="editCategoryName" required>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelCategoryEditBtn">取消</button>
                    <button type="submit" class="btn btn-primary" id="saveCategoryEditBtn">保存</button>
                </div>
            </form>
        </div>
    </div>
    
    <!-- 添加分类模态框 -->
    <div class="modal" id="addCategoryModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">添加分类</h2>
                <button class="close-modal" id="closeAddCategoryModalBtn">&times;</button>
            </div>
            <form id="addCategoryForm">
                <div class="form-group">
                    <label class="form-label" for="addCategoryName">分类名称</label>
                    <input type="text" class="form-input" id="addCategoryName" required placeholder="请输入新分类名称">
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelAddCategoryBtn">取消</button>
                    <button type="submit" class="btn btn-primary" id="saveAddCategoryBtn">添加</button>
                </div>
            </form>
        </div>
    </div>
    
    <!-- 配色和背景模态框 -->
    <div class="modal" id="colorBgModal">
        <div class="modal-content color-bg-modal-content">
            <div class="modal-header">
                <h2 class="modal-title">配色与背景</h2>
                <button class="close-modal" id="closeColorBgModalBtn">&times;</button>
            </div>
            
            <div class="color-tabs">
                <button class="color-tab active" data-tab="skins">皮肤</button>
                <button class="color-tab" data-tab="colors">颜色</button>
                <button class="color-tab" data-tab="background">背景</button>
                <button class="color-tab" data-tab="fonts">字体与标题</button>
            </div>
            
            <!-- 皮肤标签页 -->
            <div class="color-tab-content active" id="skinsTab">
                <div class="form-group">
                    <label class="form-label">选择预设皮肤</label>
                    <div class="skin-grid" id="skinGrid">
                        <!-- 皮肤将通过JS动态生成 -->
                    </div>
                    <small style="color: #666; display: block; margin-top: 10px;">提示：切换皮肤只会改变外观，不会影响您的自定义设置</small>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelSkinBtn">取消</button>
                    <button type="button" class="btn btn-primary" id="applySkinBtn">应用皮肤</button>
                </div>
            </div>
            
            <!-- 颜色标签页 -->
            <div class="color-tab-content" id="colorsTab">
                <div class="form-group">
                    <label class="form-label">自定义颜色</label>
                    
                    <div class="color-picker-container">
                        <span class="color-label">标题颜色</span>
                        <input type="color" class="custom-color-input" id="titleColorPicker" value="#ffffff">
                        <span class="color-value" id="titleColorValue">#FFFFFF</span>
                    </div>
                    
                    <div class="color-picker-container">
                        <span class="color-label">分类颜色</span>
                        <input type="color" class="custom-color-input" id="categoryColorPicker" value="#ffffff">
                        <span class="color-value" id="categoryColorValue">#FFFFFF</span>
                    </div>
                    
                    <div class="color-picker-container">
                        <span class="color-label">网站颜色</span>
                        <input type="color" class="custom-color-input" id="bookmarkColorPicker" value="#ffffff">
                        <span class="color-value" id="bookmarkColorValue">#FFFFFF</span>
                    </div>
                    
                    <div class="color-picker-container">
                        <span class="color-label">主色调</span>
                        <input type="color" class="custom-color-input" id="primaryColorPicker" value="#667eea">
                        <span class="color-value" id="primaryColorValue">#667EEA</span>
                    </div>
                    
                    <div class="color-picker-container">
                        <span class="color-label">副色调</span>
                        <input type="color" class="custom-color-input" id="secondaryColorPicker" value="#764ba2">
                        <span class="color-value" id="secondaryColorValue">#764BA2</span>
                    </div>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelColorsBtn">取消</button>
                    <button type="button" class="btn btn-primary" id="applyColorsBtn">应用颜色</button>
                </div>
            </div>
            
            <!-- 背景标签页 -->
            <div class="color-tab-content" id="backgroundTab">
                <div class="form-group">
                    <label class="form-label">选择背景类型</label>
                    <div class="bg-options">
                        <div class="bg-option" id="gradient1" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);">
                            <div class="bg-option-text">渐变1</div>
                        </div>
                        <div class="bg-option" id="gradient2" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);">
                            <div class="bg-option-text">渐变2</div>
                        </div>
                        <div class="bg-option" id="gradient3" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
                            <div class="bg-option-text">渐变3</div>
                        </div>
                        <div class="bg-option" id="gradient4" style="background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);">
                            <div class="bg-option-text">渐变4</div>
                        </div>
                        <div class="bg-option" id="gradient5" style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);">
                            <div class="bg-option-text">渐变5</div>
                        </div>
                        <div class="bg-option" id="imageUpload">
                            <div class="bg-option-text" style="color: #333;">
                                <i class="fas fa-upload"></i> 上传图片
                            </div>
                        </div>
                    </div>
                </div>
                <div class="form-group">
                    <label class="form-label">上传自定义图片 (支持4K高清壁纸)</label>
                    <input type="file" class="form-input" id="imageUploadInput" accept="image/*">
                    <div class="error-message" id="imageError"></div>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelBgBtn">取消</button>
                    <button type="button" class="btn btn-primary" id="applyBgBtn">应用背景</button>
                </div>
            </div>
            
            <!-- 字体与标题标签页 - 加宽布局 -->
            <div class="color-tab-content" id="fontsTab">
                <div class="form-group">
                    <label class="form-label">标题文字</label>
                    <input type="text" class="form-input" id="editTitleText" placeholder="请输入导航页标题">
                    <small style="color: #666; display: block; margin-top: 5px;">提示：留空可删除标题文字</small>
                </div>
                <div class="form-group">
                    <label class="form-label">副标题文字</label>
                    <input type="text" class="form-input" id="editSubtitleText" placeholder="请输入副标题">
                    <small style="color: #666; display: block; margin-top: 5px;">提示：留空可删除副标题文字</small>
                </div>
                <div class="form-group">
                    <label class="form-label">标题图标</label>
                    <div style="text-align: center;">
                        <img id="titleIconPreview" class="title-icon-preview" src="" alt="图标预览" style="display: none;">
                    </div>
                    <input type="file" class="form-input" id="titleIconUpload" accept="image/*" style="margin-bottom: 10px;">
                    <button type="button" class="btn btn-secondary" id="removeTitleIconBtn" style="width: 100%; margin-bottom: 20px;">移除图标</button>
                </div>
                <div class="form-group">
                    <label class="form-label" for="titleFontSize">标题字体大小</label>
                    <input type="range" class="form-input" id="titleFontSize" min="24" max="80" step="2" value="48">
                    <div style="display: flex; justify-content: space-between; margin-top: 5px;">
                        <span>小</span>
                        <span id="fontSizeValue">48px</span>
                        <span>大</span>
                    </div>
                </div>
                <div class="form-group">
                    <label class="form-label">标题字体</label>
                    <div class="font-selector" id="titleFontSelector">
                        <div class="font-option" data-font="Pacifico, cursive" style="font-family: 'Pacifico', cursive;">圆润体</div>
                        <div class="font-option" data-font="'Dancing Script', cursive" style="font-family: 'Dancing Script', cursive;">手写体</div>
                        <div class="font-option" data-font="'Playfair Display', serif" style="font-family: 'Playfair Display', serif;">衬线体</div>
                        <div class="font-option" data-font="'Montserrat', sans-serif" style="font-family: 'Montserrat', sans-serif;">现代体</div>
                        <div class="font-option" data-font="'Roboto', sans-serif" style="font-family: 'Roboto', sans-serif;">简洁体</div>
                        <div class="font-option" data-font="'Caveat', cursive" style="font-family: 'Caveat', cursive;">手写2体</div>
                        <div class="font-option" data-font="'Shadows Into Light', cursive" style="font-family: 'Shadows Into Light', cursive;">阴影体</div>
                        <div class="font-option" data-font="'Fredericka the Great', cursive" style="font-family: 'Fredericka the Great', cursive;">典雅体</div>
                        <div class="font-option" data-font="'Special Elite', cursive" style="font-family: 'Special Elite', cursive;">打字机体</div>
                    </div>
                </div>
                <div class="form-group">
                    <label class="form-label">副标题字体</label>
                    <div class="font-selector" id="subtitleFontSelector">
                        <div class="font-option" data-font="'Long Cang', cursive" style="font-family: 'Long Cang', cursive;">龙藏体</div>
                        <div class="font-option" data-font="'Noto Sans SC', sans-serif" style="font-family: 'Noto Sans SC', sans-serif;">思源黑体</div>
                        <div class="font-option" data-font="'ZCOOL XiaoWei', serif" style="font-family: 'ZCOOL XiaoWei', serif;">站酷小微</div>
                        <div class="font-option" data-font="'Roboto', sans-serif" style="font-family: 'Roboto', sans-serif;">Roboto</div>
                        <div class="font-option" data-font="'Montserrat', sans-serif" style="font-family: 'Montserrat', sans-serif;">Montserrat</div>
                        <div class="font-option" data-font="'Dancing Script', cursive" style="font-family: 'Dancing Script', cursive;">手写体</div>
                        <div class="font-option" data-font="'ZCOOL QingKe HuangYou', sans-serif" style="font-family: 'ZCOOL QingKe HuangYou', sans-serif;">站酷青楷</div>
                        <div class="font-option" data-font="'Ma Shan Zheng', cursive" style="font-family: 'Ma Shan Zheng', cursive;">马善政体</div>
                        <div class="font-option" data-font="'Liu Jian Mao Cao', cursive" style="font-family: 'Liu Jian Mao Cao', cursive;">刘剑毛笔</div>
                    </div>
                </div>
                <div class="form-actions">
                    <button type="button" class="btn btn-secondary" id="cancelFontsBtn">取消</button>
                    <button type="button" class="btn btn-primary" id="applyFontsBtn">应用字体与标题</button>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 管理行数模态框 -->
    <div class="modal" id="manageRowsModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">管理行数</h2>
                <button class="close-modal" id="closeManageRowsModalBtn">&times;</button>
            </div>
            <div class="form-group">
                <label class="form-label">当前行数: <span id="currentRowsCount">4</span> 行 (每行6个网站)</label>
                <div style="margin: 20px 0;">
                    <button type="button" class="btn btn-primary" id="addRowBtn" style="width: 100%; margin-bottom: 10px;">
                        <i class="fas fa-plus-circle"></i> 增加一行
                    </button>
                    <button type="button" class="btn" id="removeRowBtn" style="width: 100%; background: #ff6b6b; color: white;">
                        <i class="fas fa-minus-circle"></i> 减少一行
                    </button>
                </div>
                <div class="error-message" id="rowsError"></div>
                <small style="color: #666; display: block; margin-top: 10px;">提示：每行显示6个网站，最少1行，最多8行</small>
            </div>
            <div class="form-actions">
                <button type="button" class="btn btn-secondary" id="cancelManageRowsBtn">关闭</button>
            </div>
        </div>
    </div>
    
    <!-- 导入导出模态框 -->
    <div class="modal" id="importExportModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">数据备份与恢复</h2>
                <button class="close-modal" id="closeImportExportModalBtn">&times;</button>
            </div>
            <div class="form-group">
                <label class="form-label">导出数据</label>
                <p style="margin-bottom: 10px; color: #666;">点击下方按钮将当前所有数据导出为TXT文件</p>
                <button type="button" class="btn btn-primary" id="exportDataBtn" style="width: 100%;">
                    <i class="fas fa-download"></i> 导出数据到TXT文件
                </button>
            </div>
            <div class="form-group">
                <label class="form-label">导入数据</label>
                <p style="margin-bottom: 10px; color: #666;">将导出的TXT文件内容粘贴到下方，或选择文件导入</p>
                <textarea class="data-textarea" id="importDataText" placeholder="请粘贴导出的TXT内容..."></textarea>
                <input type="file" class="form-input" id="importFileInput" accept=".txt" style="margin-bottom: 10px;">
                <div class="error-message" id="importError"></div>
                <small style="color: #666; display: block; margin-top: 5px;">提示：导入前会自动备份当前数据到"自动备份_当前时间.txt"</small>
            </div>
            <div class="form-actions">
                <button type="button" class="btn btn-secondary" id="cancelImportExportBtn">取消</button>
                <button type="button" class="btn btn-primary" id="importDataBtn">导入数据</button>
            </div>
        </div>
    </div>

    <!-- 确认对话框 -->
    <div class="modal" id="confirmDialog">
        <div class="confirm-dialog">
            <div class="confirm-title" id="confirmDialogTitle">确认操作</div>
            <div class="confirm-message" id="confirmDialogMessage">您确定要执行此操作吗？</div>
            <div class="confirm-actions">
                <button type="button" class="btn btn-secondary" id="confirmDialogCancelBtn">取消</button>
                <button type="button" class="btn btn-primary" id="confirmDialogConfirmBtn">确认</button>
            </div>
        </div>
    </div>

    <!-- 管理行数选择对话框 -->
    <div class="modal" id="rowsApplyModal">
        <div class="modal-content" style="max-width: 400px;">
            <div class="modal-header">
                <h2 class="modal-title">应用到页面</h2>
                <button class="close-modal" id="closeRowsApplyModalBtn">&times;</button>
            </div>
            <div class="form-group">
                <label class="form-label" style="text-align: center; margin-bottom: 20px;">请选择将此更改应用到哪个页面：</label>
                <div style="display: flex; gap: 10px; margin-top: 10px;">
                    <button type="button" class="btn" id="applyToCurrentPageBtn" style="flex: 1; background: var(--primary-color); color: white;">当前页面</button>
                    <button type="button" class="btn" id="applyToAllPagesBtn" style="flex: 1; background: #4CAF50; color: white;">所有页面</button>
                </div>
            </div>
            <div class="form-actions">
                <button type="button" class="btn btn-secondary" id="cancelRowsApplyBtn">取消</button>
            </div>
        </div>
    </div>

    <script>
        // 搜索框提示语数组
        const searchPlaceholders = [
            "喂，是直接搜还是走个流程？",
            "告诉我你想翻谁的牌子～",
            "别愣着，敲点字吧！",
            "网址或咒语，速速报来。",
            "知识、八卦、好玩的，我全知道。",
            "您的专属任意门，请输入目的地。",
            "偷偷告诉我，你想搜什么？",
            "开始一场'即搜即走'的旅行。",
            "我准备好了，你呢？",
            "输入任意'愿望'，开始生成。",
            "启动一次关键词穿越。",
            "请输入目的地坐标（或关键词）。",
            "连接你与答案的最近节点。",
            "将你的好奇，编译为地址。",
            "思想发射井，等待指令。",
            "您的大脑外接搜索引擎，已就绪。",
            "从这里，打开下一个标签页。",
            "用几个字，撬动整个网络。",
            "当前路径：未定义。请输入新路径。",
            "问题接收器，正在待命。",
            "指尖所向，山海皆可往。",
            "在此处，投石问路。",
            "让一个词，带你抵达它的辽阔。",
            "心念一动，世界便为你铺路。",
            "方寸之间，自有天地。",
            "所有的远方，都始于此刻的光标。",
            "以词为舟，以网为海。",
            "书写你的下一个'抵达'。",
            "凝神，输入，然后抵达。",
            "每一次回车，都是启程。",
            "愣着干嘛？填它！",
            "知识、八卦、好玩的，我全知道。",
            "您的专属任意门，请输入目的地。",
            "悄悄话模式：你想搜什么？",
            "开始一场'即搜即走'的旅行。",
            "万事俱备，只差你的输入。",
            "输入任意'愿望'，开始生成。",
            "叮！这里接收所有问题。",
            "思想发射井，等待指令。",
            "您的大脑外接搜索引擎，已就绪。",
            "从这里，打开下一个标签页。",
            "用几个字，撬动整个网络。",
            "当前路径：未定义。请输入新路径。",
            "问题接收器，正在待命。",
            "向未知发送一个信号。",
            "启动你的信息火箭。",
            "心念一动，世界便为你铺路。",
            "方寸之间，自有天地。",
            "所有的远方，都始于此刻的光标。",
            "以词为舟，以网为海。",
            "书写你的下一个'抵达'。",
            "凝神，输入，然后抵达。",
            "近来搜得甚妙？",
            "心有一念，此处落键。",
            "但书一字，海内共鸣。",
            "欲叩何方门扉？",
            "忽有所得？书于此。",
            "游目骋怀，以此为棹。",
            "啪！你要搜个什么？",
            "万川映月，一月摄万川。",
            "搜山搜海，不如搜心。",
            "莫问搜否，但管敲来。"
        ];

        // 预设皮肤数据 - 修改：替换柠檬黄为白色亮色系，修复星空紫颜色
        const skinPresets = [
            {
                id: 'skin1',
                name: '深邃蓝',
                primaryColor: '#667eea',
                secondaryColor: '#764ba2',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff'
            },
            {
                id: 'skin2',
                name: '梦幻粉',
                primaryColor: '#f093fb',
                secondaryColor: '#f5576c',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff'
            },
            {
                id: 'skin3',
                name: '海洋蓝',
                primaryColor: '#4facfe',
                secondaryColor: '#00f2fe',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff'
            },
            {
                id: 'skin4',
                name: '森林绿',
                primaryColor: '#43e97b',
                secondaryColor: '#38f9d7',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #43e97b 0%, #38f9d7 100%)',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff'
            },
            {
                id: 'skin5',
                name: '落日橙',
                primaryColor: '#fa709a',
                secondaryColor: '#fee140',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)',
                textColor: '#333333',
                categoryColor: '#333333',
                bookmarkColor: '#333333'
            },
            {
                id: 'skin6',
                name: '简约黑',
                primaryColor: '#333333',
                secondaryColor: '#666666',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #333333 0%, #666666 100%)',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff'
            },
            {
                id: 'skin7',
                name: '薰衣草',
                primaryColor: '#a8edea',
                secondaryColor: '#fed6e3',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)',
                textColor: '#333333',
                categoryColor: '#333333',
                bookmarkColor: '#333333'
            },
            {
                id: 'skin8',
                name: '纯净白',
                primaryColor: '#f8f9fa',
                secondaryColor: '#e9ecef',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%)',
                textColor: '#333333',
                categoryColor: '#333333',
                bookmarkColor: '#333333'
            },
            {
                id: 'skin9',
                name: '星空紫',
                primaryColor: '#6a11cb',
                secondaryColor: '#2575fc',
                bgType: 'gradient',
                bgValue: 'linear-gradient(135deg, #6a11cb 0%, #2575fc 100%)',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff'
            }
        ];

        // 初始数据
        const initialData = {
            categories: [
                { id: 1, name: '尔联', order: 1 },
                { id: 2, name: '影音', order: 2 },
                { id: 3, name: '购物', order: 3 },
                { id: 4, name: '资讯', order: 4 },
                { id: 5, name: '社交', order: 5 },
                { id: 6, name: '生活', order: 6 },
                { id: 7, name: '工具', order: 7 },
                { id: 8, name: 'IT', order: 8 },
                { id: 9, name: '趣站', order: 9 },
                { id: 10, name: '学习', order: 10 },
                { id: 11, name: '工作', order: 11 }
            ],
            bookmarks: [
                // 尔联分类 - 用户提供的网站
                { id: 1, name: '携程供应商', url: 'https://vbooking.ctrip.com/ivbk/accountV2/login', categoryId: 1, order: 1, customIcon: null },
                { id: 2, name: 'Odoo', url: 'https://crm.ulinktravel.com.tr/web/login', categoryId: 1, order: 2, customIcon: null },
                { id: 3, name: '飞猪用车', url: 'https://sell.fliggy.com/transcrs/index#/orders', categoryId: 1, order: 3, customIcon: null },
                { id: 4, name: '飞猪店铺', url: 'https://work.taobao.com/', categoryId: 1, order: 4, customIcon: null },
                { id: 5, name: 'Whatsapp', url: 'https://www.whatsapp.com/', categoryId: 1, order: 5, customIcon: null },
                { id: 6, name: 'Get Transfer', url: 'https://gettransfer.com/zh/carrier/#/cabinet/requests', categoryId: 1, order: 6, customIcon: null },
                { id: 7, name: 'Viator', url: 'https://supplier.viator.com/?logout=true', categoryId: 1, order: 7, customIcon: null },
                { id: 8, name: '企业微信邮箱', url: 'https://work.weixin.qq.com/mail/', categoryId: 1, order: 8, customIcon: null },
                { id: 9, name: '谷歌翻译', url: 'https://translate.google.com/', categoryId: 1, order: 9, customIcon: null },
                { id: 10, name: '谷歌地图', url: 'https://www.google.com/maps', categoryId: 1, order: 10, customIcon: null },
                { id: 11, name: 'Dida用车', url: 'https://tna-supplier-int.didatravel.com/order', categoryId: 1, order: 11, customIcon: null },
                { id: 12, name: 'Omacar', url: 'http://fleets.omacar.com/', categoryId: 1, order: 12, customIcon: null },
                { id: 13, name: '圣索菲亚大教堂', url: 'https://agency.demmuseums.com/Authentication/SignIn', categoryId: 1, order: 13, customIcon: null },
                { id: 14, name: '地下水宫', url: 'https://www.passo.com.tr/tr/mekan/yerebatan-sarnici-muzeleri-bilet/719215', categoryId: 1, order: 14, customIcon: null },
                { id: 15, name: '旋转舞', url: 'https://www.hodjapasha.com/sistem/login.php', categoryId: 1, order: 15, customIcon: null },
                { id: 16, name: '综合出票', url: 'https://muze.gov.tr/ETicket', categoryId: 1, order: 16, customIcon: null },
                { id: 17, name: '新皇宫-多尔玛巴赫切', url: 'https://acente.millisaraylar.gov.tr/Home/Index', categoryId: 1, order: 17, customIcon: null },
                { id: 18, name: '海峡游船', url: 'https://www.turyol.com/', categoryId: 1, order: 18, customIcon: null },
                { id: 19, name: 'TK-土耳其航空', url: 'https://www.turkishairlines.com/', categoryId: 1, order: 19, customIcon: null },
                { id: 20, name: 'PC-飞马航空', url: 'http://www.flypgs.com', categoryId: 1, order: 20, customIcon: null },
                { id: 21, name: 'XQ-太阳快运', url: 'http://www.sunexpress.com', categoryId: 1, order: 21, customIcon: null },
                { id: 22, name: 'VF-AJET', url: 'https://ajet.com/tr', categoryId: 1, order: 22, customIcon: null },
                { id: 23, name: '机票B2B', url: 'https://acente.biletbank.com/', categoryId: 1, order: 23, customIcon: null },
                { id: 24, name: '土耳其签证', url: 'https://dtvgroup.com.tr/', categoryId: 1, order: 24, customIcon: null },
                
                // 影音分类 - 24个网站
                { id: 25, name: '哔哩哔哩', url: 'https://www.bilibili.com', categoryId: 2, order: 1, customIcon: null },
                { id: 26, name: 'YouTube', url: 'https://www.youtube.com', categoryId: 2, order: 2, customIcon: null },
                { id: 27, name: '爱奇艺', url: 'https://www.iqiyi.com', categoryId: 2, order: 3, customIcon: null },
                { id: 28, name: '腾讯视频', url: 'https://v.qq.com', categoryId: 2, order: 4, customIcon: null },
                { id: 29, name: '优酷', url: 'https://www.youku.com', categoryId: 2, order: 5, customIcon: null },
                { id: 30, name: '芒果TV', url: 'https://www.mgtv.com', categoryId: 2, order: 6, customIcon: null },
                { id: 31, name: '网易云音乐', url: 'https://music.163.com', categoryId: 2, order: 7, customIcon: null },
                { id: 32, name: 'QQ音乐', url: 'https://y.qq.com', categoryId: 2, order: 8, customIcon: null },
                { id: 33, name: '酷狗音乐', url: 'https://www.kugou.com', categoryId: 2, order: 9, customIcon: null },
                { id: 34, name: '酷我音乐', url: 'https://www.kuwo.cn', categoryId: 2, order: 10, customIcon: null },
                { id: 35, name: '咪咕音乐', url: 'https://music.migu.cn', categoryId: 2, order: 11, customIcon: null },
                { id: 36, name: '抖音', url: 'https://www.douyin.com', categoryId: 2, order: 12, customIcon: null },
                { id: 37, name: '快手', url: 'https://www.kuaishou.com', categoryId: 2, order: 13, customIcon: null },
                { id: 38, name: '斗鱼', url: 'https://www.douyu.com', categoryId: 2, order: 14, customIcon: null },
                { id: 39, name: '虎牙直播', url: 'https://www.huya.com', categoryId: 2, order: 15, customIcon: null },
                { id: 40, name: 'AcFun', url: 'https://www.acfun.cn', categoryId: 2, order: 16, customIcon: null },
                { id: 41, name: '西瓜视频', url: 'https://www.ixigua.com', categoryId: 2, order: 17, customIcon: null },
                { id: 42, name: '喜马拉雅', url: 'https://www.ximalaya.com', categoryId: 2, order: 18, customIcon: null },
                { id: 43, name: '蜻蜓FM', url: 'https://www.qingting.fm', categoryId: 2, order: 19, customIcon: null },
                { id: 44, name: '猫耳FM', url: 'https://www.missevan.com', categoryId: 2, order: 20, customIcon: null },
                { id: 45, name: '全民K歌', url: 'https://kg.qq.com', categoryId: 2, order: 21, customIcon: null },
                { id: 46, name: '唱吧', url: 'https://changba.com', categoryId: 2, order: 22, customIcon: null },
                { id: 47, name: '网易LOOK直播', url: 'https://look.163.com', categoryId: 2, order: 23, customIcon: null },
                { id: 48, name: '微光', url: 'https://weiguang.com', categoryId: 2, order: 24, customIcon: null },
                
                // 购物分类 - 24个网站
                { id: 49, name: '淘宝', url: 'https://www.taobao.com', categoryId: 3, order: 1, customIcon: null },
                { id: 50, name: '天猫', url: 'https://www.tmall.com', categoryId: 3, order: 2, customIcon: null },
                { id: 51, name: '京东', url: 'https://www.jd.com', categoryId: 3, order: 3, customIcon: null },
                { id: 52, name: '拼多多', url: 'https://www.pinduoduo.com', categoryId: 3, order: 4, customIcon: null },
                { id: 53, name: '苏宁易购', url: 'https://www.suning.com', categoryId: 3, order: 5, customIcon: null },
                { id: 54, name: '唯品会', url: 'https://www.vip.com', categoryId: 3, order: 6, customIcon: null },
                { id: 55, name: '考拉海购', url: 'https://www.kaola.com', categoryId: 3, order: 7, customIcon: null },
                { id: 56, name: '亚马逊中国', url: 'https://www.amazon.cn', categoryId: 3, order: 8, customIcon: null },
                { id: 57, name: '小米有品', url: 'https://www.xiaomiyoupin.com', categoryId: 3, order: 9, customIcon: null },
                { id: 58, name: '网易严选', url: 'https://you.163.com', categoryId: 3, order: 10, customIcon: null },
                { id: 59, name: '当当网', url: 'https://www.dangdang.com', categoryId: 3, order: 11, customIcon: null },
                { id: 60, name: '国美在线', url: 'https://www.gome.com.cn', categoryId: 3, order: 12, customIcon: null },
                { id: 61, name: '1号店', url: 'https://www.yhd.com', categoryId: 3, order: 13, customIcon: null },
                { id: 62, name: '蘑菇街', url: 'https://www.mogujie.com', categoryId: 3, order: 14, customIcon: null },
                { id: 63, name: '聚美优品', url: 'https://www.jumei.com', categoryId: 3, order: 15, customIcon: null },
                { id: 64, name: '返利网', url: 'https://www.fanli.com', categoryId: 3, order: 16, customIcon: null },
                { id: 65, name: '什么值得买', url: 'https://www.smzdm.com', categoryId: 3, order: 17, customIcon: null },
                { id: 66, name: '小红书', url: 'https://www.xiaohongshu.com', categoryId: 3, order: 18, customIcon: null },
                { id: 67, name: '得物', url: 'https://www.dewu.com', categoryId: 3, order: 19, customIcon: null },
                { id: 68, name: '寺库', url: 'https://www.secoo.com', categoryId: 3, order: 20, customIcon: null },
                { id: 69, name: '洋码头', url: 'https://www.ymatou.com', categoryId: 3, order: 21, customIcon: null },
                { id: 70, name: '蜜芽', url: 'https://www.mia.com', categoryId: 3, order: 22, customIcon: null },
                { id: 71, name: '贝贝网', url: 'https://www.beibei.com', categoryId: 3, order: 23, customIcon: null },
                { id: 72, name: '卷皮网', url: 'https://www.juanpi.com', categoryId: 3, order: 24, customIcon: null },
                
                // 资讯分类 - 24个网站
                { id: 73, name: '新浪新闻', url: 'https://news.sina.com.cn', categoryId: 4, order: 1, customIcon: null },
                { id: 74, name: '网易新闻', url: 'https://news.163.com', categoryId: 4, order: 2, customIcon: null },
                { id: 75, name: '腾讯新闻', url: 'https://news.qq.com', categoryId: 4, order: 3, customIcon: null },
                { id: 76, name: '搜狐新闻', url: 'https://news.sohu.com', categoryId: 4, order: 4, customIcon: null },
                { id: 77, name: '今日头条', url: 'https://www.toutiao.com', categoryId: 4, order: 5, customIcon: null },
                { id: 78, name: '凤凰网', url: 'https://www.ifeng.com', categoryId: 4, order: 6, customIcon: null },
                { id: 79, name: '澎湃新闻', url: 'https://www.thepaper.cn', categoryId: 4, order: 7, customIcon: null },
                { id: 80, name: '界面新闻', url: 'https://www.jiemian.com', categoryId: 4, order: 8, customIcon: null },
                { id: 81, name: '虎嗅', url: 'https://www.huxiu.com', categoryId: 4, order: 9, customIcon: null },
                { id: 82, name: '36氪', url: 'https://www.36kr.com', categoryId: 4, order: 10, customIcon: null },
                { id: 83, name: '钛媒体', url: 'https://www.tmtpost.com', categoryId: 4, order: 11, customIcon: null },
                { id: 84, name: '爱范儿', url: 'https://www.ifanr.com', categoryId: 4, order: 12, customIcon: null },
                { id: 85, name: '知乎', url: 'https://www.zhihu.com', categoryId: 4, order: 13, customIcon: null },
                { id: 86, name: '豆瓣', url: 'https://www.douban.com', categoryId: 4, order: 14, customIcon: null },
                { id: 87, name: '简书', url: 'https://www.jianshu.com', categoryId: 4, order: 15, customIcon: null },
                { id: 88, name: '果壳', url: 'https://www.guokr.com', categoryId: 4, order: 16, customIcon: null },
                { id: 89, name: '雪球', url: 'https://xueqiu.com', categoryId: 4, order: 17, customIcon: null },
                { id: 90, name: '东方财富', url: 'https://www.eastmoney.com', categoryId: 4, order: 18, customIcon: null },
                { id: 91, name: '同花顺', url: 'https://www.10jqka.com.cn', categoryId: 4, order: 19, customIcon: null },
                { id: 92, name: '财新网', url: 'https://www.caixin.com', categoryId: 4, order: 20, customIcon: null },
                { id: 93, name: '华尔街见闻', url: 'https://wallstreetcn.com', categoryId: 4, order: 21, customIcon: null },
                { id: 94, name: '新浪财经', url: 'https://finance.sina.com.cn', categoryId: 4, order: 22, customIcon: null },
                { id: 95, name: '央视网', url: 'https://www.cctv.com', categoryId: 4, order: 23, customIcon: null },
                { id: 96, name: '人民网', url: 'https://www.people.com.cn', categoryId: 4, order: 24, customIcon: null },
                
                // 社交分类 - 24个网站
                { id: 97, name: '微信', url: 'https://wx.qq.com', categoryId: 5, order: 1, customIcon: null },
                { id: 98, name: 'QQ', url: 'https://im.qq.com', categoryId: 5, order: 2, customIcon: null },
                { id: 99, name: '微博', url: 'https://weibo.com', categoryId: 5, order: 3, customIcon: null },
                { id: 100, name: '贴吧', url: 'https://tieba.baidu.com', categoryId: 5, order: 4, customIcon: null },
                { id: 101, name: '知乎', url: 'https://www.zhihu.com', categoryId: 5, order: 5, customIcon: null },
                { id: 102, name: '豆瓣', url: 'https://www.douban.com', categoryId: 5, order: 6, customIcon: null },
                { id: 103, name: '小红书', url: 'https://www.xiaohongshu.com', categoryId: 5, order: 7, customIcon: null },
                { id: 104, name: '陌陌', url: 'https://www.immomo.com', categoryId: 5, order: 8, customIcon: null },
                { id: 105, name: '探探', url: 'https://www.tantanapp.com', categoryId: 5, order: 9, customIcon: null },
                { id: 106, name: 'Soul', url: 'https://www.soulapp.cn', categoryId: 5, order: 10, customIcon: null },
                { id: 107, name: '脉脉', url: 'https://maimai.cn', categoryId: 5, order: 11, customIcon: null },
                { id: 108, name: '领英', url: 'https://www.linkedin.com', categoryId: 5, order: 12, customIcon: null },
                { id: 109, name: '钉钉', url: 'https://www.dingtalk.com', categoryId: 5, order: 13, customIcon: null },
                { id: 110, name: '飞书', url: 'https://www.feishu.cn', categoryId: 5, order: 14, customIcon: null },
                { id: 111, name: '企业微信', url: 'https://work.weixin.qq.com', categoryId: 5, order: 15, customIcon: null },
                { id: 112, name: 'YY', url: 'https://www.yy.com', categoryId: 5, order: 16, customIcon: null },
                { id: 113, name: '虎牙直播', url: 'https://www.huya.com', categoryId: 5, order: 17, customIcon: null },
                { id: 114, name: '斗鱼', url: 'https://www.douyu.com', categoryId: 5, order: 18, customIcon: null },
                { id: 115, name: 'Blued', url: 'https://www.blued.com', categoryId: 5, order: 19, customIcon: null },
                { id: 116, name: '比心', url: 'https://www.bixin.com', categoryId: 5, order: 20, customIcon: null },
                { id: 117, name: '积目', url: 'https://www.jimu.com', categoryId: 5, order: 21, customIcon: null },
                { id: 118, name: 'Uki', url: 'https://www.uki.com', categoryId: 5, order: 22, customIcon: null },
                { id: 119, name: '伊对', url: 'https://www.yidui.com', categoryId: 5, order: 23, customIcon: null },
                { id: 120, name: '世纪佳缘', url: 'https://www.jiayuan.com', categoryId: 5, order: 24, customIcon: null },
                
                // 生活分类 - 24个网站
                { id: 121, name: '下厨房', url: 'https://www.xiachufang.com', categoryId: 6, order: 1, customIcon: null },
                { id: 122, name: '大众点评', url: 'https://www.dianping.com', categoryId: 6, order: 2, customIcon: null },
                { id: 123, name: '美团', url: 'https://www.meituan.com', categoryId: 6, order: 3, customIcon: null },
                { id: 124, name: '饿了么', url: 'https://www.ele.me', categoryId: 6, order: 4, customIcon: null },
                { id: 125, name: '菜鸟裹裹', url: 'https://www.cainiao.com', categoryId: 6, order: 5, customIcon: null },
                { id: 126, name: '快递100', url: 'https://www.kuaidi100.com', categoryId: 6, order: 6, customIcon: null },
                { id: 127, name: '天气通', url: 'https://tianqi.qq.com', categoryId: 6, order: 7, customIcon: null },
                { id: 128, name: '墨迹天气', url: 'https://www.moji.com', categoryId: 6, order: 8, customIcon: null },
                { id: 129, name: '丁香医生', url: 'https://dxy.com', categoryId: 6, order: 9, customIcon: null },
                { id: 130, name: '好大夫在线', url: 'https://www.haodf.com', categoryId: 6, order: 10, customIcon: null },
                { id: 131, name: '汽车之家', url: 'https://www.autohome.com.cn', categoryId: 6, order: 11, customIcon: null },
                { id: 132, name: '易车', url: 'https://www.bitauto.com', categoryId: 6, order: 12, customIcon: null },
                { id: 133, name: '链家', url: 'https://www.lianjia.com', categoryId: 6, order: 13, customIcon: null },
                { id: 134, name: '安居客', url: 'https://www.anjuke.com', categoryId: 6, order: 14, customIcon: null },
                { id: 135, name: '马蜂窝', url: 'https://www.mafengwo.cn', categoryId: 6, order: 15, customIcon: null },
                { id: 136, name: '携程旅行', url: 'https://www.ctrip.com', categoryId: 6, order: 16, customIcon: null },
                { id: 137, name: '去哪儿', url: 'https://www.qunar.com', categoryId: 6, order: 17, customIcon: null },
                { id: 138, name: '途牛', url: 'https://www.tuniu.com', categoryId: 6, order: 18, customIcon: null },
                { id: 139, name: '飞猪', url: 'https://www.fliggy.com', categoryId: 6, order: 19, customIcon: null },
                { id: 140, name: '神州租车', url: 'https://www.zuche.com', categoryId: 6, order: 20, customIcon: null },
                { id: 141, name: '滴滴出行', url: 'https://www.didiglobal.com', categoryId: 6, order: 21, customIcon: null },
                { id: 142, name: '高德地图', url: 'https://www.amap.com', categoryId: 6, order: 22, customIcon: null },
                { id: 143, name: '百度地图', url: 'https://map.baidu.com', categoryId: 6, order: 23, customIcon: null },
                { id: 144, name: '掌上生活', url: 'https://xyk.cmbchina.com', categoryId: 6, order: 24, customIcon: null },
                
                // 工具分类 - 24个网站
                { id: 145, name: '百度网盘', url: 'https://pan.baidu.com', categoryId: 7, order: 1, customIcon: null },
                { id: 146, name: '腾讯微云', url: 'https://www.weiyun.com', categoryId: 7, order: 2, customIcon: null },
                { id: 147, name: '金山文档', url: 'https://www.kdocs.cn', categoryId: 7, order: 3, customIcon: null },
                { id: 148, name: '石墨文档', url: 'https://shimo.im', categoryId: 7, order: 4, customIcon: null },
                { id: 149, name: '腾讯文档', url: 'https://docs.qq.com', categoryId: 7, order: 5, customIcon: null },
                { id: 150, name: '有道云笔记', url: 'https://note.youdao.com', categoryId: 7, order: 6, customIcon: null },
                { id: 151, name: '印象笔记', url: 'https://www.yinxiang.com', categoryId: 7, order: 7, customIcon: null },
                { id: 152, name: '幕布', url: 'https://mubu.com', categoryId: 7, order: 8, customIcon: null },
                { id: 153, name: 'ProcessOn', url: 'https://www.processon.com', categoryId: 7, order: 9, customIcon: null },
                { id: 154, name: 'Canva可画', url: 'https://www.canva.cn', categoryId: 7, order: 10, customIcon: null },
                { id: 155, name: '稿定设计', url: 'https://www.gaoding.com', categoryId: 7, order: 11, customIcon: null },
                { id: 156, name: '创客贴', url: 'https://www.chuangkit.com', categoryId: 7, order: 12, customIcon: null },
                { id: 157, name: '蓝湖', url: 'https://lanhuapp.com', categoryId: 7, order: 13, customIcon: null },
                { id: 158, name: '码云', url: 'https://gitee.com', categoryId: 7, order: 14, customIcon: null },
                { id: 159, name: 'GitHub', url: 'https://github.com', categoryId: 7, order: 15, customIcon: null },
                { id: 160, name: '站长工具', url: 'https://tool.chinaz.com', categoryId: 7, order: 16, customIcon: null },
                { id: 161, name: '阿里云', url: 'https://www.aliyun.com', categoryId: 7, order: 17, customIcon: null },
                { id: 162, name: '腾讯云', url: 'https://cloud.tencent.com', categoryId: 7, order: 18, customIcon: null },
                { id: 163, name: '华为云', url: 'https://www.huaweicloud.com', categoryId: 7, order: 19, customIcon: null },
                { id: 164, name: '百度统计', url: 'https://tongji.baidu.com', categoryId: 7, order: 20, customIcon: null },
                { id: 165, name: '友盟+', url: 'https://www.umeng.com', categoryId: 7, order: 21, customIcon: null },
                { id: 166, name: '七牛云', url: 'https://www.qiniu.com', categoryId: 7, order: 22, customIcon: null },
                { id: 167, name: '又拍云', url: 'https://www.upyun.com', categoryId: 7, order: 23, customIcon: null },
                { id: 168, name: '腾讯问卷', url: 'https://wj.qq.com', categoryId: 7, order: 24, customIcon: null },
                
                // IT分类 - 24个网站
                { id: 169, name: 'CSDN', url: 'https://www.csdn.net', categoryId: 8, order: 1, customIcon: null },
                { id: 170, name: '博客园', url: 'https://www.cnblogs.com', categoryId: 8, order: 2, customIcon: null },
                { id: 171, name: '掘金', url: 'https://juejin.cn', categoryId: 8, order: 3, customIcon: null },
                { id: 172, name: 'SegmentFault', url: 'https://segmentfault.com', categoryId: 8, order: 4, customIcon: null },
                { id: 173, name: '开源中国', url: 'https://www.oschina.net', categoryId: 8, order: 5, customIcon: null },
                { id: 174, name: 'V2EX', url: 'https://www.v2ex.com', categoryId: 8, order: 6, customIcon: null },
                { id: 175, name: 'Stack Overflow', url: 'https://stackoverflow.com', categoryId: 8, order: 7, customIcon: null },
                { id: 176, name: 'LeetCode', url: 'https://leetcode.cn', categoryId: 8, order: 8, customIcon: null },
                { id: 177, name: '牛客网', url: 'https://www.nowcoder.com', categoryId: 8, order: 9, customIcon: null },
                { id: 178, name: '实验楼', url: 'https://www.shiyanlou.com', categoryId: 8, order: 10, customIcon: null },
                { id: 179, name: '慕课网', url: 'https://www.imooc.com', categoryId: 8, order: 11, customIcon: null },
                { id: 180, name: '极客时间', url: 'https://time.geekbang.org', categoryId: 8, order: 12, customIcon: null },
                { id: 181, name: '网易云课堂', url: 'https://study.163.com', categoryId: 8, order: 13, customIcon: null },
                { id: 182, name: '腾讯课堂', url: 'https://ke.qq.com', categoryId: 8, order: 14, customIcon: null },
                { id: 183, name: '51CTO', url: 'https://www.51cto.com', categoryId: 8, order: 15, customIcon: null },
                { id: 184, name: 'InfoQ', url: 'https://www.infoq.cn', categoryId: 8, order: 16, customIcon: null },
                { id: 185, name: 'IT之家', url: 'https://www.ithome.com', categoryId: 8, order: 17, customIcon: null },
                { id: 186, name: '少数派', url: 'https://sspai.com', categoryId: 8, order: 18, customIcon: null },
                { id: 187, name: 'Product Hunt', url: 'https://www.producthunt.com', categoryId: 8, order: 19, customIcon: null },
                { id: 188, name: 'Hacker News', url: 'https://news.ycombinator.com', categoryId: 8, order: 20, customIcon: null },
                { id: 189, name: 'Dev.to', url: 'https://dev.to', categoryId: 8, order: 21, customIcon: null },
                { id: 190, name: 'Medium', url: 'https://medium.com', categoryId: 8, order: 22, customIcon: null },
                { id: 191, name: 'Dribbble', url: 'https://dribbble.com', categoryId: 8, order: 23, customIcon: null },
                { id: 192, name: 'Behance', url: 'https://www.behance.net', categoryId: 8, order: 24, customIcon: null },
                
                // 趣站分类 - 24个网站
                { id: 193, name: '有意思吧', url: 'https://www.u148.net', categoryId: 9, order: 1, customIcon: null },
                { id: 194, name: '煎蛋', url: 'https://jandan.net', categoryId: 9, order: 2, customIcon: null },
                { id: 195, name: '糗事百科', url: 'https://www.qiushibaike.com', categoryId: 9, order: 3, customIcon: null },
                { id: 196, name: '暴走漫画', url: 'https://www.baozou.com', categoryId: 9, order: 4, customIcon: null },
                { id: 197, name: 'ACG导航', url: 'https://www.acgndog.com', categoryId: 9, order: 5, customIcon: null },
                { id: 198, name: '漫画人', url: 'https://www.manhuaren.com', categoryId: 9, order: 6, customIcon: null },
                { id: 199, name: '有妖气', url: 'https://www.u17.com', categoryId: 9, order: 7, customIcon: null },
                { id: 200, name: '快看漫画', url: 'https://www.kuaikanmanhua.com', categoryId: 9, order: 8, customIcon: null },
                { id: 201, name: '动漫之家', url: 'https://www.dmzj.com', categoryId: 9, order: 9, customIcon: null },
                { id: 202, name: 'B站番剧', url: 'https://www.bilibili.com/anime', categoryId: 9, order: 10, customIcon: null },
                { id: 203, name: '网易漫画', url: 'https://manhua.163.com', categoryId: 9, order: 11, customIcon: null },
                { id: 204, name: '腾讯动漫', url: 'https://ac.qq.com', categoryId: 9, order: 12, customIcon: null },
                { id: 205, name: '知音漫客', url: 'https://www.zymk.cn', categoryId: 9, order: 13, customIcon: null },
                { id: 206, name: '漫画台', url: 'https://www.manhuatai.com', categoryId: 9, order: 14, customIcon: null },
                { id: 207, name: '咚漫', url: 'https://www.dongmanmanhua.cn', categoryId: 9, order: 15, customIcon: null },
                { id: 208, name: '漫漫漫画', url: 'https://www.manmanapp.com', categoryId: 9, order: 16, customIcon: null },
                { id: 209, name: '漫画岛', url: 'https://www.manhuadao.cn', categoryId: 9, order: 17, customIcon: null },
                { id: 210, name: '看漫画', url: 'https://www.kanman.com', categoryId: 9, order: 18, customIcon: null },
                { id: 211, name: '微博动漫', url: 'https://manhua.weibo.com', categoryId: 9, order: 19, customIcon: null },
                { id: 212, name: '漫画人', url: 'https://www.manhuaren.com', categoryId: 9, order: 20, customIcon: null },
                { id: 213, name: '动漫屋', url: 'https://www.dm5.com', categoryId: 9, order: 21, customIcon: null },
                { id: 214, name: '鼠绘漫画', url: 'https://www.ishuhui.com', categoryId: 9, order: 22, customIcon: null },
                { id: 215, name: '汗汗漫画', url: 'https://www.hhmmoo.com', categoryId: 9, order: 23, customIcon: null },
                { id: 216, name: '漫画堆', url: 'https://www.manhuadui.com', categoryId: 9, order: 24, customIcon: null },
                
                // 学习分类 - 24个网站
                { id: 217, name: '中国大学MOOC', url: 'https://www.icourse163.org', categoryId: 10, order: 1, customIcon: null },
                { id: 218, name: '学堂在线', url: 'https://www.xuetangx.com', categoryId: 10, order: 2, customIcon: null },
                { id: 219, name: '网易公开课', url: 'https://open.163.com', categoryId: 10, order: 3, customIcon: null },
                { id: 220, name: 'TED', url: 'https://www.ted.com', categoryId: 10, order: 4, customIcon: null },
                { id: 221, name: 'Coursera', url: 'https://www.coursera.org', categoryId: 10, order: 5, customIcon: null },
                { id: 222, name: 'edX', url: 'https://www.edx.org', categoryId: 10, order: 6, customIcon: null },
                { id: 223, name: 'Udacity', url: 'https://www.udacity.com', categoryId: 10, order: 7, customIcon: null },
                { id: 224, name: 'Khan Academy', url: 'https://www.khanacademy.org', categoryId: 10, order: 8, customIcon: null },
                { id: 225, name: '可汗学院', url: 'https://zh.khanacademy.org', categoryId: 10, order: 9, customIcon: null },
                { id: 226, name: '多邻国', url: 'https://www.duolingo.com', categoryId: 10, order: 10, customIcon: null },
                { id: 227, name: '扇贝单词', url: 'https://www.shanbay.com', categoryId: 10, order: 11, customIcon: null },
                { id: 228, name: '百词斩', url: 'https://www.baicizhan.com', categoryId: 10, order: 12, customIcon: null },
                { id: 229, name: '沪江网校', url: 'https://www.hujiang.com', categoryId: 10, order: 13, customIcon: null },
                { id: 230, name: '小站教育', url: 'https://www.zhan.com', categoryId: 10, order: 14, customIcon: null },
                { id: 231, name: '新东方在线', url: 'https://www.koolearn.com', categoryId: 10, order: 15, customIcon: null },
                { id: 232, name: '学而思网校', url: 'https://www.xueersi.com', categoryId: 10, order: 16, customIcon: null },
                { id: 233, name: '作业帮', url: 'https://www.zybang.com', categoryId: 10, order: 17, customIcon: null },
                { id: 234, name: '猿辅导', url: 'https://www.yuanfudao.com', categoryId: 10, order: 18, customIcon: null },
                { id: 235, name: '跟谁学', url: 'https://www.genshuixue.com', categoryId: 10, order: 19, customIcon: null },
                { id: 236, name: 'VIPKID', url: 'https://www.vipkid.com.cn', categoryId: 10, order: 20, customIcon: null },
                { id: 237, name: 'DaDa英语', url: 'https://www.dadaabc.com', categoryId: 10, order: 21, customIcon: null },
                { id: 238, name: '51Talk', url: 'https://www.51talk.com', categoryId: 10, order: 22, customIcon: null },
                { id: 239, name: '流利说', url: 'https://www.liulishuo.com', categoryId: 10, order: 23, customIcon: null },
                { id: 240, name: '英语趣配音', url: 'https://www.qupeiyin.com', categoryId: 10, order: 24, customIcon: null },
                
                // 工作分类 - 24个网站
                { id: 241, name: 'BOSS直聘', url: 'https://www.zhipin.com', categoryId: 11, order: 1, customIcon: null },
                { id: 242, name: '拉勾网', url: 'https://www.lagou.com', categoryId: 11, order: 2, customIcon: null },
                { id: 243, name: '智联招聘', url: 'https://www.zhaopin.com', categoryId: 11, order: 3, customIcon: null },
                { id: 244, name: '前程无忧', url: 'https://www.51job.com', categoryId: 11, order: 4, customIcon: null },
                { id: 245, name: '猎聘', url: 'https://www.liepin.com', categoryId: 11, order: 5, customIcon: null },
                { id: 246, name: '大街网', url: 'https://www.dajie.com', categoryId: 11, order: 6, customIcon: null },
                { id: 247, name: '应届生求职网', url: 'https://www.yingjiesheng.com', categoryId: 11, order: 7, customIcon: null },
                { id: 248, name: '实习僧', url: 'https://www.shixiseng.com', categoryId: 11, order: 8, customIcon: null },
                { id: 249, name: '看准网', url: 'https://www.kanzhun.com', categoryId: 11, order: 9, customIcon: null },
                { id: 250, name: '企查查', url: 'https://www.qichacha.com', categoryId: 11, order: 10, customIcon: null },
                { id: 251, name: '天眼查', url: 'https://www.tianyancha.com', categoryId: 11, order: 11, customIcon: null },
                { id: 252, name: '启信宝', url: 'https://www.qixin.com', categoryId: 11, order: 12, customIcon: null },
                { id: 253, name: '国家企业信用信息', url: 'https://www.gsxt.gov.cn', categoryId: 11, order: 13, customIcon: null },
                { id: 254, name: '企查猫', url: 'https://www.qichamao.com', categoryId: 11, order: 14, customIcon: null },
                { id: 255, name: '公司宝', url: 'https://www.gongsibao.com', categoryId: 11, order: 15, customIcon: null },
                { id: 256, name: '金蝶', url: 'https://www.kingdee.com', categoryId: 11, order: 16, customIcon: null },
                { id: 257, name: '用友', url: 'https://www.yonyou.com', categoryId: 11, order: 17, customIcon: null },
                { id: 258, name: 'SAP', url: 'https://www.sap.com', categoryId: 11, order: 18, customIcon: null },
                { id: 259, name: 'Oracle', url: 'https://www.oracle.com', categoryId: 11, order: 19, customIcon: null },
                { id: 260, name: 'Salesforce', url: 'https://www.salesforce.com', categoryId: 11, order: 20, customIcon: null },
                { id: 261, name: 'Workday', url: 'https://www.workday.com', categoryId: 11, order: 21, customIcon: null },
                { id: 262, name: 'Zoom', url: 'https://zoom.us', categoryId: 11, order: 22, customIcon: null },
                { id: 263, name: 'Teams', url: 'https://www.microsoft.com/teams', categoryId: 11, order: 23, customIcon: null },
                { id: 264, name: 'Slack', url: 'https://slack.com', categoryId: 11, order: 24, customIcon: null }
            ],
            settings: {
                backgroundType: 'gradient',
                backgroundValue: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
                primaryColor: '#667eea',
                secondaryColor: '#764ba2',
                pageTitle: '屿间',
                pageSubtitle: '每一次与过往照面，都是为了与未来更好地相逢。',
                pageTitleIcon: '',
                pageTitleFontSize: '48px',
                pageTitleFont: 'Pacifico, cursive',
                pageSubtitleFont: "'Long Cang', cursive",
                searchEngine: 'google',
                textColor: '#ffffff',
                categoryColor: '#ffffff',
                bookmarkColor: '#ffffff',
                rowsPerCategory: 4,
                currentPage: 1
            }
        };

        // 隐藏页初始数据
        const hiddenInitialData = JSON.parse(JSON.stringify(initialData));
        hiddenInitialData.settings.currentPage = 2;

        // 状态管理
        let state = {
            categories: [],
            bookmarks: [],
            settings: {},
            currentCategory: null,
            editingBookmarkId: null,
            editingCategoryId: null,
            selectedSkin: null,
            editMode: false,
            showSettingsMenu: false,
            searchEngines: {
                google: { name: '谷歌', icon: 'fab fa-google', color: '#4285f4', url: 'https://www.google.com/search?q=' },
                baidu: { name: '百度', icon: 'fab fa-baidu', color: '#2932e1', url: 'https://www.baidu.com/s?wd=' },
                bing: { name: 'Bing', icon: 'fab fa-microsoft', color: '#008373', url: 'https://www.bing.com/search?q=' },
                yandex: { name: 'Yandex', icon: 'fas fa-y', color: '#ff0000', url: 'https://yandex.com/search/?text=' },
                duckduckgo: { name: 'DuckDuckGo', icon: 'fas fa-search', color: '#de5833', url: 'https://duckduckgo.com/?q=' },
                youtube: { name: 'YouTube', icon: 'fab fa-youtube', color: '#ff0000', url: 'https://www.youtube.com/results?search_query=' },
                netease: { name: '网易云', icon: 'fas fa-music', color: '#e60026', url: 'https://music.163.com/#/search/m/?s=' },
                sogou: { name: '搜狗', icon: 'fas fa-search', color: '#ff5500', url: 'https://www.sogou.com/web?query=' },
                zhihu: { name: '知乎', icon: 'fab fa-zhihu', color: '#0084ff', url: 'https://www.zhihu.com/search?type=content&q=' },
                biying: { name: '必应', icon: 'fab fa-microsoft', color: '#008373', url: 'https://cn.bing.com/search?q=' },
                bilibili: { name: 'B站', icon: 'fab fa-bilibili', color: '#fb7299', url: 'https://search.bilibili.com/all?keyword=' },
                all: { name: '综合搜索', icon: 'fas fa-globe', color: '#666666', url: 'https://www.dogedoge.com/results?q=' }
            },
            faviconCache: {},
            currentAction: null,
            settingsBtnMode: 'settings',
            defaultIcons: [
                { class: 'fas fa-search icon-search', category: '搜索' },
                { class: 'fab fa-google icon-search', category: '搜索' },
                { class: 'fab fa-baidu icon-search', category: '搜索' },
                { class: 'fab fa-youtube icon-video', category: '视频' },
                { class: 'fab fa-bilibili icon-video', category: '视频' },
                { class: 'fab fa-facebook icon-social', category: '社交' },
                { class: 'fab fa-twitter icon-social', category: '社交' },
                { class: 'fab fa-weixin icon-social', category: '社交' },
                { class: 'fas fa-shopping-cart icon-shopping', category: '购物' },
                { class: 'fab fa-amazon icon-shopping', category: '购物' },
                { class: 'fab fa-alipay icon-finance', category: '金融' },
                { class: 'fas fa-plane icon-travel', category: '旅行' },
                { class: 'fas fa-hotel icon-travel', category: '旅行' },
                { class: 'fas fa-briefcase icon-work', category: '工作' },
                { class: 'fas fa-graduation-cap icon-education', category: '教育' },
                { class: 'fas fa-gamepad icon-games', category: '游戏' },
                { class: 'fas fa-music icon-music', category: '音乐' },
                { class: 'fas fa-film icon-video', category: '视频' },
                { class: 'fas fa-newspaper icon-news', category: '新闻' },
                { class: 'fas fa-wrench icon-tools', category: '工具' },
                { class: 'fas fa-utensils icon-food', category: '美食' },
                { class: 'fas fa-heartbeat icon-health', category: '健康' },
                { class: 'fas fa-code icon-tech', category: '技术' },
                { class: 'fas fa-futbol icon-sports', category: '体育' },
                { class: 'fas fa-cloud-sun icon-weather', category: '天气' },
                { class: 'fas fa-book icon-books', category: '书籍' },
                { class: 'fas fa-palette icon-art', category: '艺术' },
                { class: 'fas fa-camera icon-art', category: '艺术' }
            ],
            draggingCategoryId: null,
            draggingBookmarkId: null,
            titleIconPreview: null,
            isHiddenPage: false,
            hiddenData: {
                categories: [],
                bookmarks: [],
                settings: {}
            },
            rowsChangeAction: null,
            rowsChangeCount: 0,
            rowsApplyTarget: null
        };

        // DOM元素
        const elements = {
            mainContainer: document.getElementById('mainContainer'),
            hiddenContainer: document.getElementById('hiddenContainer'),
            categoriesContainer: document.getElementById('categoriesContainer'),
            hiddenCategoriesContainer: document.getElementById('hiddenCategoriesContainer'),
            bookmarksContainer: document.getElementById('bookmarksContainer'),
            hiddenBookmarksContainer: document.getElementById('hiddenBookmarksContainer'),
            editBookmarkModal: document.getElementById('editBookmarkModal'),
            editCategoryModal: document.getElementById('editCategoryModal'),
            addCategoryModal: document.getElementById('addCategoryModal'),
            colorBgModal: document.getElementById('colorBgModal'),
            manageRowsModal: document.getElementById('manageRowsModal'),
            importExportModal: document.getElementById('importExportModal'),
            backgroundImage: document.getElementById('backgroundImage'),
            pageTitle: document.getElementById('pageTitle'),
            pageSubtitle: document.getElementById('pageSubtitle'),
            hiddenPageTitle: document.getElementById('hiddenPageTitle'),
            hiddenPageSubtitle: document.getElementById('hiddenPageSubtitle'),
            searchInput: document.getElementById('searchInput'),
            hiddenSearchInput: document.getElementById('hiddenSearchInput'),
            currentEngine: document.getElementById('currentEngine'),
            hiddenCurrentEngine: document.getElementById('hiddenCurrentEngine'),
            engineGrid: document.getElementById('engineGrid'),
            hiddenEngineGrid: document.getElementById('hiddenEngineGrid'),
            searchBtn: document.getElementById('searchBtn'),
            hiddenSearchBtn: document.getElementById('hiddenSearchBtn'),
            settingsBtn: document.getElementById('settingsBtn'),
            settingsMenu: document.getElementById('settingsMenu'),
            customizeBtn: document.getElementById('customizeBtn'),
            colorBgBtn: document.getElementById('colorBgBtn'),
            importExportBtn: document.getElementById('importExportBtn'),
            resetBtn: document.getElementById('resetBtn'),
            closeImportExportModalBtn: document.getElementById('closeImportExportModalBtn'),
            exportDataBtn: document.getElementById('exportDataBtn'),
            importDataText: document.getElementById('importDataText'),
            importFileInput: document.getElementById('importFileInput'),
            importDataBtn: document.getElementById('importDataBtn'),
            cancelImportExportBtn: document.getElementById('cancelImportExportBtn'),
            importError: document.getElementById('importError'),
            dragHint: document.getElementById('dragHint'),
            hiddenDragHint: document.getElementById('hiddenDragHint'),
            iconSelector: document.getElementById('iconSelector'),
            imageError: document.getElementById('imageError'),
            titleIconPreview: document.getElementById('titleIconPreview'),
            titleIconUpload: document.getElementById('titleIconUpload'),
            removeTitleIconBtn: document.getElementById('removeTitleIconBtn'),
            editTitleText: document.getElementById('editTitleText'),
            editSubtitleText: document.getElementById('editSubtitleText'),
            titleFontSize: document.getElementById('titleFontSize'),
            fontSizeValue: document.getElementById('fontSizeValue'),
            pageSwitcherRight: document.getElementById('pageSwitcherRight'),
            pageSwitcherLeft: document.getElementById('pageSwitcherLeft'),
            pageIndicator: document.getElementById('pageIndicator'),
            skinGrid: document.getElementById('skinGrid'),
            currentRowsCount: document.getElementById('currentRowsCount'),
            addRowBtn: document.getElementById('addRowBtn'),
            removeRowBtn: document.getElementById('removeRowBtn'),
            saveManageRowsBtn: document.getElementById('saveManageRowsBtn'),
            rowsError: document.getElementById('rowsError'),
            confirmDialog: document.getElementById('confirmDialog'),
            confirmDialogTitle: document.getElementById('confirmDialogTitle'),
            confirmDialogMessage: document.getElementById('confirmDialogMessage'),
            confirmDialogCancelBtn: document.getElementById('confirmDialogCancelBtn'),
            confirmDialogConfirmBtn: document.getElementById('confirmDialogConfirmBtn'),
            rowsApplyModal: document.getElementById('rowsApplyModal'),
            closeRowsApplyModalBtn: document.getElementById('closeRowsApplyModalBtn'),
            applyToCurrentPageBtn: document.getElementById('applyToCurrentPageBtn'),
            applyToAllPagesBtn: document.getElementById('applyToAllPagesBtn'),
            cancelRowsApplyBtn: document.getElementById('cancelRowsApplyBtn')
        };

        // 初始化应用
        function initApp() {
            loadData();
            renderSearchEngines();
            renderCategories();
            applySettings();
            setupEventListeners();
            
            // 确保第一个分类默认显示
            if (state.categories.length > 0) {
                state.currentCategory = state.categories[0].id;
                setActiveCategory(state.currentCategory, true);
                renderBookmarks();
            }
            
            // 更新搜索引擎显示
            updateSearchEngineDisplay();
            
            // 预加载现有书签的favicon
            preloadFavicons();
            
            // 渲染图标选择器
            renderIconSelector();
            
            // 渲染皮肤选择器
            renderSkinGrid();
            
            // 设置随机搜索框提示语
            setRandomSearchPlaceholder();
            
            // 初始化颜色选择器
            setupColorPickers();
            
            // 初始化字体选择器
            setupFontSelectors();
            
            // 初始化隐藏页
            initHiddenPage();
        }

        // 初始化隐藏页
        function initHiddenPage() {
            loadHiddenData();
            renderHiddenSearchEngines();
            renderHiddenCategories();
            applyHiddenSettings();
            
            if (state.hiddenData.categories.length > 0) {
                state.hiddenData.currentCategory = state.hiddenData.categories[0].id;
                setHiddenActiveCategory(state.hiddenData.currentCategory, true);
                renderHiddenBookmarks();
            }
            
            updateHiddenSearchEngineDisplay();
            
            // 设置隐藏页搜索框提示语
            setHiddenRandomSearchPlaceholder();
        }

        // 设置随机搜索框提示语
        function setRandomSearchPlaceholder() {
            if (searchPlaceholders && searchPlaceholders.length > 0) {
                const randomIndex = Math.floor(Math.random() * searchPlaceholders.length);
                elements.searchInput.placeholder = searchPlaceholders[randomIndex];
            }
        }

        function setHiddenRandomSearchPlaceholder() {
            if (searchPlaceholders && searchPlaceholders.length > 0) {
                const randomIndex = Math.floor(Math.random() * searchPlaceholders.length);
                elements.hiddenSearchInput.placeholder = searchPlaceholders[randomIndex];
            }
        }

        // 预加载favicon
        async function preloadFavicons() {
            for (const bookmark of state.bookmarks) {
                if (!state.faviconCache[bookmark.url]) {
                    await getFavicon(bookmark.url);
                }
            }
        }

        // 获取网站favicon
        async function getFavicon(url) {
            if (state.faviconCache[url]) {
                return state.faviconCache[url];
            }
            
            try {
                const domain = new URL(url).hostname;
                const faviconUrl = `https://www.google.com/s2/favicons?domain=${domain}&sz=32`;
                
                const img = new Image();
                await new Promise((resolve, reject) => {
                    img.onload = () => resolve(faviconUrl);
                    img.onerror = () => reject();
                    img.src = faviconUrl;
                });
                
                state.faviconCache[url] = faviconUrl;
                return faviconUrl;
            } catch (error) {
                state.faviconCache[url] = null;
                return null;
            }
        }

        // 加载数据
        function loadData() {
            const savedData = localStorage.getItem('navPageData');
            
            if (savedData) {
                const parsedData = JSON.parse(savedData);
                state.categories = parsedData.categories || initialData.categories;
                state.bookmarks = parsedData.bookmarks || initialData.bookmarks;
                state.settings = parsedData.settings || initialData.settings;
                
                // 确保设置存在
                ensureSettings();
                
                // 恢复favicon缓存
                if (parsedData.faviconCache) {
                    state.faviconCache = parsedData.faviconCache;
                }
                
                // 确保书签有自定义图标字段
                state.bookmarks.forEach(bookmark => {
                    if (!bookmark.customIcon) {
                        bookmark.customIcon = null;
                    }
                });
                
                // 确保order字段
                ensureOrderFields();
            } else {
                state.categories = [...initialData.categories];
                state.bookmarks = [...initialData.bookmarks];
                state.settings = {...initialData.settings};
                ensureSettings();
                saveData();
            }
        }

        // 加载隐藏页数据
        function loadHiddenData() {
            const savedData = localStorage.getItem('navPageHiddenData');
            
            if (savedData) {
                const parsedData = JSON.parse(savedData);
                state.hiddenData.categories = parsedData.categories || hiddenInitialData.categories;
                state.hiddenData.bookmarks = parsedData.bookmarks || hiddenInitialData.bookmarks;
                state.hiddenData.settings = parsedData.settings || hiddenInitialData.settings;
                
                // 确保设置存在
                ensureHiddenSettings();
                
                // 确保书签有自定义图标字段
                state.hiddenData.bookmarks.forEach(bookmark => {
                    if (!bookmark.customIcon) {
                        bookmark.customIcon = null;
                    }
                });
                
                // 确保order字段
                ensureHiddenOrderFields();
            } else {
                state.hiddenData.categories = [...hiddenInitialData.categories];
                state.hiddenData.bookmarks = [...hiddenInitialData.bookmarks];
                state.hiddenData.settings = {...hiddenInitialData.settings};
                ensureHiddenSettings();
                saveHiddenData();
            }
        }

        // 确保设置存在
        function ensureSettings() {
            const defaults = initialData.settings;
            if (!state.settings.rowsPerCategory) state.settings.rowsPerCategory = defaults.rowsPerCategory;
            if (!state.settings.textColor) state.settings.textColor = defaults.textColor;
            if (!state.settings.categoryColor) state.settings.categoryColor = defaults.categoryColor;
            if (!state.settings.bookmarkColor) state.settings.bookmarkColor = defaults.bookmarkColor;
            if (!state.settings.pageTitleIcon) state.settings.pageTitleIcon = defaults.pageTitleIcon;
            if (!state.settings.pageTitleFontSize) state.settings.pageTitleFontSize = defaults.pageTitleFontSize;
            if (!state.settings.pageTitleFont) state.settings.pageTitleFont = defaults.pageTitleFont;
            if (!state.settings.pageSubtitle) state.settings.pageSubtitle = defaults.pageSubtitle;
            if (!state.settings.pageSubtitleFont) state.settings.pageSubtitleFont = defaults.pageSubtitleFont;
            if (!state.settings.currentPage) state.settings.currentPage = defaults.currentPage;
        }

        function ensureHiddenSettings() {
            const defaults = hiddenInitialData.settings;
            if (!state.hiddenData.settings.rowsPerCategory) state.hiddenData.settings.rowsPerCategory = defaults.rowsPerCategory;
            if (!state.hiddenData.settings.textColor) state.hiddenData.settings.textColor = defaults.textColor;
            if (!state.hiddenData.settings.categoryColor) state.hiddenData.settings.categoryColor = defaults.categoryColor;
            if (!state.hiddenData.settings.bookmarkColor) state.hiddenData.settings.bookmarkColor = defaults.bookmarkColor;
            if (!state.hiddenData.settings.pageTitleIcon) state.hiddenData.settings.pageTitleIcon = defaults.pageTitleIcon;
            if (!state.hiddenData.settings.pageTitleFontSize) state.hiddenData.settings.pageTitleFontSize = defaults.pageTitleFontSize;
            if (!state.hiddenData.settings.pageTitleFont) state.hiddenData.settings.pageTitleFont = defaults.pageTitleFont;
            if (!state.hiddenData.settings.pageSubtitle) state.hiddenData.settings.pageSubtitle = defaults.pageSubtitle;
            if (!state.hiddenData.settings.pageSubtitleFont) state.hiddenData.settings.pageSubtitleFont = defaults.pageSubtitleFont;
            if (!state.hiddenData.settings.currentPage) state.hiddenData.settings.currentPage = defaults.currentPage;
        }

        // 确保order字段存在
        function ensureOrderFields() {
            state.categories.sort((a, b) => (a.order || 0) - (b.order || 0));
            state.categories.forEach((category, index) => {
                if (!category.order) {
                    category.order = index + 1;
                }
            });
            
            const bookmarksByCategory = {};
            state.bookmarks.forEach(bookmark => {
                if (!bookmarksByCategory[bookmark.categoryId]) {
                    bookmarksByCategory[bookmark.categoryId] = [];
                }
                bookmarksByCategory[bookmark.categoryId].push(bookmark);
            });
            
            Object.keys(bookmarksByCategory).forEach(categoryId => {
                bookmarksByCategory[categoryId].sort((a, b) => (a.order || 0) - (b.order || 0));
                bookmarksByCategory[categoryId].forEach((bookmark, index) => {
                    bookmark.order = index + 1;
                });
            });
        }

        function ensureHiddenOrderFields() {
            state.hiddenData.categories.sort((a, b) => (a.order || 0) - (b.order || 0));
            state.hiddenData.categories.forEach((category, index) => {
                if (!category.order) {
                    category.order = index + 1;
                }
            });
            
            const bookmarksByCategory = {};
            state.hiddenData.bookmarks.forEach(bookmark => {
                if (!bookmarksByCategory[bookmark.categoryId]) {
                    bookmarksByCategory[bookmark.categoryId] = [];
                }
                bookmarksByCategory[bookmark.categoryId].push(bookmark);
            });
            
            Object.keys(bookmarksByCategory).forEach(categoryId => {
                bookmarksByCategory[categoryId].sort((a, b) => (a.order || 0) - (b.order || 0));
                bookmarksByCategory[categoryId].forEach((bookmark, index) => {
                    bookmark.order = index + 1;
                });
            });
        }

        // 保存数据
        function saveData() {
            const dataToSave = {
                categories: state.categories,
                bookmarks: state.bookmarks,
                settings: state.settings,
                faviconCache: state.faviconCache
            };
            localStorage.setItem('navPageData', JSON.stringify(dataToSave));
        }

        function saveHiddenData() {
            const dataToSave = {
                categories: state.hiddenData.categories,
                bookmarks: state.hiddenData.bookmarks,
                settings: state.hiddenData.settings
            };
            localStorage.setItem('navPageHiddenData', JSON.stringify(dataToSave));
        }

        // 渲染搜索引擎
        function renderSearchEngines() {
            elements.engineGrid.innerHTML = '';
            
            Object.entries(state.searchEngines).forEach(([key, engine]) => {
                const item = document.createElement('div');
                item.className = 'engine-grid-item';
                item.dataset.engine = key;
                item.style.color = engine.color;
                
                item.innerHTML = `
                    <div class="engine-grid-icon">
                        <i class="${engine.icon}" style="color: ${engine.color}"></i>
                    </div>
                    <div class="engine-grid-name">${engine.name}</div>
                `;
                
                item.addEventListener('click', () => {
                    if (state.editMode) return;
                    state.settings.searchEngine = key;
                    saveData();
                    updateSearchEngineDisplay();
                    elements.engineGrid.classList.remove('show');
                });
                
                elements.engineGrid.appendChild(item);
            });
        }

        function renderHiddenSearchEngines() {
            elements.hiddenEngineGrid.innerHTML = '';
            
            Object.entries(state.searchEngines).forEach(([key, engine]) => {
                const item = document.createElement('div');
                item.className = 'engine-grid-item';
                item.dataset.engine = key;
                item.style.color = engine.color;
                
                item.innerHTML = `
                    <div class="engine-grid-icon">
                        <i class="${engine.icon}" style="color: ${engine.color}"></i>
                    </div>
                    <div class="engine-grid-name">${engine.name}</div>
                `;
                
                item.addEventListener('click', () => {
                    if (state.editMode) return;
                    state.hiddenData.settings.searchEngine = key;
                    saveHiddenData();
                    updateHiddenSearchEngineDisplay();
                    elements.hiddenEngineGrid.classList.remove('show');
                });
                
                elements.hiddenEngineGrid.appendChild(item);
            });
        }

        // 渲染图标选择器
        function renderIconSelector() {
            elements.iconSelector.innerHTML = '';
            
            const iconsByCategory = {};
            state.defaultIcons.forEach(icon => {
                if (!iconsByCategory[icon.category]) {
                    iconsByCategory[icon.category] = [];
                }
                iconsByCategory[icon.category].push(icon);
            });
            
            Object.keys(iconsByCategory).forEach(category => {
                const categoryTitle = document.createElement('div');
                categoryTitle.style.gridColumn = '1 / -1';
                categoryTitle.style.fontSize = '12px';
                categoryTitle.style.color = '#666';
                categoryTitle.style.marginTop = '10px';
                categoryTitle.style.marginBottom = '5px';
                categoryTitle.textContent = category;
                elements.iconSelector.appendChild(categoryTitle);
                
                iconsByCategory[category].forEach(icon => {
                    const iconOption = document.createElement('div');
                    iconOption.className = 'icon-option';
                    iconOption.innerHTML = `<i class="${icon.class}"></i>`;
                    iconOption.dataset.icon = icon.class;
                    iconOption.title = category;
                    
                    iconOption.addEventListener('click', () => {
                        document.querySelectorAll('.icon-option').forEach(option => {
                            option.classList.remove('selected');
                        });
                        iconOption.classList.add('selected');
                    });
                    
                    elements.iconSelector.appendChild(iconOption);
                });
            });
        }

        // 渲染皮肤网格
        function renderSkinGrid() {
            elements.skinGrid.innerHTML = '';
            
            skinPresets.forEach(skin => {
                const skinItem = document.createElement('div');
                skinItem.className = 'skin-item';
                skinItem.dataset.skin = skin.id;
                
                skinItem.innerHTML = `
                    <div class="skin-preview" style="background: ${skin.bgValue}; color: ${skin.textColor === '#ffffff' ? 'white' : '#333'};">
                        ${skin.name}
                    </div>
                    <div class="skin-name">${skin.name}</div>
                `;
                
                skinItem.addEventListener('click', () => {
                    document.querySelectorAll('.skin-item').forEach(item => {
                        item.classList.remove('selected');
                    });
                    skinItem.classList.add('selected');
                    state.selectedSkin = skin;
                });
                
                elements.skinGrid.appendChild(skinItem);
            });
        }

        // 设置颜色选择器
        function setupColorPickers() {
            // 标题颜色
            const titleColorPicker = document.getElementById('titleColorPicker');
            const titleColorValue = document.getElementById('titleColorValue');
            titleColorPicker.value = state.settings.textColor;
            titleColorValue.textContent = state.settings.textColor.toUpperCase();
            
            titleColorPicker.addEventListener('input', (e) => {
                titleColorValue.textContent = e.target.value.toUpperCase();
            });
            
            // 分类颜色
            const categoryColorPicker = document.getElementById('categoryColorPicker');
            const categoryColorValue = document.getElementById('categoryColorValue');
            categoryColorPicker.value = state.settings.categoryColor;
            categoryColorValue.textContent = state.settings.categoryColor.toUpperCase();
            
            categoryColorPicker.addEventListener('input', (e) => {
                categoryColorValue.textContent = e.target.value.toUpperCase();
            });
            
            // 网站颜色
            const bookmarkColorPicker = document.getElementById('bookmarkColorPicker');
            const bookmarkColorValue = document.getElementById('bookmarkColorValue');
            bookmarkColorPicker.value = state.settings.bookmarkColor;
            bookmarkColorValue.textContent = state.settings.bookmarkColor.toUpperCase();
            
            bookmarkColorPicker.addEventListener('input', (e) => {
                bookmarkColorValue.textContent = e.target.value.toUpperCase();
            });
            
            // 主色调
            const primaryColorPicker = document.getElementById('primaryColorPicker');
            const primaryColorValue = document.getElementById('primaryColorValue');
            primaryColorPicker.value = state.settings.primaryColor;
            primaryColorValue.textContent = state.settings.primaryColor.toUpperCase();
            
            primaryColorPicker.addEventListener('input', (e) => {
                primaryColorValue.textContent = e.target.value.toUpperCase();
            });
            
            // 副色调
            const secondaryColorPicker = document.getElementById('secondaryColorPicker');
            const secondaryColorValue = document.getElementById('secondaryColorValue');
            secondaryColorPicker.value = state.settings.secondaryColor;
            secondaryColorValue.textContent = state.settings.secondaryColor.toUpperCase();
            
            secondaryColorPicker.addEventListener('input', (e) => {
                secondaryColorValue.textContent = e.target.value.toUpperCase();
            });
        }

        // 设置字体选择器
        function setupFontSelectors() {
            // 标题字体
            const titleFontSelector = document.getElementById('titleFontSelector');
            titleFontSelector.querySelectorAll('.font-option').forEach(option => {
                option.style.fontFamily = option.dataset.font;
                option.addEventListener('click', () => {
                    titleFontSelector.querySelectorAll('.font-option').forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    option.classList.add('selected');
                });
                
                if (option.dataset.font === state.settings.pageTitleFont) {
                    option.classList.add('selected');
                }
            });
            
            // 副标题字体
            const subtitleFontSelector = document.getElementById('subtitleFontSelector');
            subtitleFontSelector.querySelectorAll('.font-option').forEach(option => {
                option.style.fontFamily = option.dataset.font;
                option.addEventListener('click', () => {
                    subtitleFontSelector.querySelectorAll('.font-option').forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    option.classList.add('selected');
                });
                
                if (option.dataset.font === state.settings.pageSubtitleFont) {
                    option.classList.add('selected');
                }
            });
        }

        // 渲染分类
        function renderCategories() {
            elements.categoriesContainer.innerHTML = '';
            
            const sortedCategories = [...state.categories].sort((a, b) => a.order - b.order);
            
            sortedCategories.forEach(category => {
                const categoryItem = document.createElement('div');
                categoryItem.className = 'category-item';
                categoryItem.dataset.id = category.id;
                categoryItem.dataset.order = category.order;
                
                if (state.editMode) {
                    categoryItem.classList.add('edit-mode');
                    categoryItem.draggable = true;
                    
                    // 拖拽事件监听器
                    setupCategoryDragEvents(categoryItem, category.id);
                }
                
                const editButtons = document.createElement('div');
                editButtons.className = 'category-edit-buttons';
                editButtons.innerHTML = `
                    <button class="edit-btn-small delete-category-btn" data-id="${category.id}">
                        <i class="fas fa-trash"></i>
                    </button>
                    <button class="edit-btn-small rename-category-btn" data-id="${category.id}">
                        <i class="fas fa-edit"></i>
                    </button>
                `;
                
                const button = document.createElement('button');
                button.className = 'category-btn';
                if (category.id === state.currentCategory) {
                    button.classList.add('active');
                }
                button.textContent = category.name;
                button.dataset.id = category.id;
                
                button.addEventListener('click', () => {
                    setActiveCategory(category.id);
                });
                
                categoryItem.appendChild(editButtons);
                categoryItem.appendChild(button);
                elements.categoriesContainer.appendChild(categoryItem);
            });
            
            if (state.editMode) {
                const addButton = document.createElement('button');
                addButton.className = 'add-category-btn';
                addButton.innerHTML = '<i class="fas fa-plus"></i> 添加分类';
                addButton.addEventListener('click', openAddCategoryModal);
                elements.categoriesContainer.appendChild(addButton);
            }
            
            // 为编辑按钮添加事件监听器
            document.querySelectorAll('.delete-category-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    const categoryId = parseInt(btn.dataset.id);
                    deleteCategory(categoryId);
                });
            });
            
            document.querySelectorAll('.rename-category-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    const categoryId = parseInt(btn.dataset.id);
                    openEditCategoryModal(categoryId);
                });
            });
        }

        function renderHiddenCategories() {
            elements.hiddenCategoriesContainer.innerHTML = '';
            
            const sortedCategories = [...state.hiddenData.categories].sort((a, b) => a.order - b.order);
            
            sortedCategories.forEach(category => {
                const categoryItem = document.createElement('div');
                categoryItem.className = 'category-item';
                categoryItem.dataset.id = category.id;
                categoryItem.dataset.order = category.order;
                
                if (state.editMode && state.isHiddenPage) {
                    categoryItem.classList.add('edit-mode');
                    categoryItem.draggable = true;
                    
                    // 拖拽事件监听器
                    setupHiddenCategoryDragEvents(categoryItem, category.id);
                }
                
                const editButtons = document.createElement('div');
                editButtons.className = 'category-edit-buttons';
                editButtons.innerHTML = `
                    <button class="edit-btn-small delete-category-btn" data-id="${category.id}">
                        <i class="fas fa-trash"></i>
                    </button>
                    <button class="edit-btn-small rename-category-btn" data-id="${category.id}">
                        <i class="fas fa-edit"></i>
                    </button>
                `;
                
                const button = document.createElement('button');
                button.className = 'category-btn';
                if (category.id === state.hiddenData.currentCategory) {
                    button.classList.add('active');
                }
                button.textContent = category.name;
                button.dataset.id = category.id;
                
                button.addEventListener('click', () => {
                    setHiddenActiveCategory(category.id);
                });
                
                categoryItem.appendChild(editButtons);
                categoryItem.appendChild(button);
                elements.hiddenCategoriesContainer.appendChild(categoryItem);
            });
            
            if (state.editMode && state.isHiddenPage) {
                const addButton = document.createElement('button');
                addButton.className = 'add-category-btn';
                addButton.innerHTML = '<i class="fas fa-plus"></i> 添加分类';
                addButton.addEventListener('click', openHiddenAddCategoryModal);
                elements.hiddenCategoriesContainer.appendChild(addButton);
            }
            
            // 为编辑按钮添加事件监听器
            elements.hiddenCategoriesContainer.querySelectorAll('.delete-category-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    const categoryId = parseInt(btn.dataset.id);
                    deleteHiddenCategory(categoryId);
                });
            });
            
            elements.hiddenCategoriesContainer.querySelectorAll('.rename-category-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    e.stopPropagation();
                    const categoryId = parseInt(btn.dataset.id);
                    openHiddenEditCategoryModal(categoryId);
                });
            });
        }

        // 设置分类拖拽事件
        function setupCategoryDragEvents(categoryItem, categoryId) {
            categoryItem.addEventListener('dragstart', (e) => {
                state.draggingCategoryId = categoryId;
                categoryItem.classList.add('dragging');
                e.dataTransfer.setData('text/plain', categoryId);
                e.dataTransfer.effectAllowed = 'move';
            });
            
            categoryItem.addEventListener('dragover', (e) => {
                e.preventDefault();
                e.dataTransfer.dropEffect = 'move';
                categoryItem.classList.add('dragging-pulse');
            });
            
            categoryItem.addEventListener('dragenter', (e) => {
                if (state.draggingCategoryId !== categoryId) {
                    categoryItem.style.border = '2px dashed rgba(255, 255, 255, 0.5)';
                    categoryItem.style.transform = 'scale(1.05)';
                }
            });
            
            categoryItem.addEventListener('dragleave', (e) => {
                categoryItem.style.border = 'none';
                categoryItem.style.transform = 'scale(1)';
                categoryItem.classList.remove('dragging-pulse');
            });
            
            categoryItem.addEventListener('drop', (e) => {
                e.preventDefault();
                categoryItem.style.border = 'none';
                categoryItem.style.transform = 'scale(1)';
                categoryItem.classList.remove('dragging-pulse');
                
                if (state.draggingCategoryId && state.draggingCategoryId !== categoryId) {
                    const draggingCategory = state.categories.find(c => c.id === state.draggingCategoryId);
                    const targetCategory = state.categories.find(c => c.id === categoryId);
                    
                    if (draggingCategory && targetCategory) {
                        const tempOrder = draggingCategory.order;
                        draggingCategory.order = targetCategory.order;
                        targetCategory.order = tempOrder;
                        
                        saveData();
                        renderCategories();
                    }
                }
            });
            
            categoryItem.addEventListener('dragend', (e) => {
                categoryItem.classList.remove('dragging');
                categoryItem.classList.remove('dragging-pulse');
                document.querySelectorAll('.category-item').forEach(item => {
                    item.style.border = 'none';
                    item.style.transform = 'scale(1)';
                });
                state.draggingCategoryId = null;
            });
        }

        function setupHiddenCategoryDragEvents(categoryItem, categoryId) {
            categoryItem.addEventListener('dragstart', (e) => {
                state.draggingCategoryId = categoryId;
                categoryItem.classList.add('dragging');
                e.dataTransfer.setData('text/plain', categoryId);
                e.dataTransfer.effectAllowed = 'move';
            });
            
            categoryItem.addEventListener('dragover', (e) => {
                e.preventDefault();
                e.dataTransfer.dropEffect = 'move';
                categoryItem.classList.add('dragging-pulse');
            });
            
            categoryItem.addEventListener('dragenter', (e) => {
                if (state.draggingCategoryId !== categoryId) {
                    categoryItem.style.border = '2px dashed rgba(255, 255, 255, 0.5)';
                    categoryItem.style.transform = 'scale(1.05)';
                }
            });
            
            categoryItem.addEventListener('dragleave', (e) => {
                categoryItem.style.border = 'none';
                categoryItem.style.transform = 'scale(1)';
                categoryItem.classList.remove('dragging-pulse');
            });
            
            categoryItem.addEventListener('drop', (e) => {
                e.preventDefault();
                categoryItem.style.border = 'none';
                categoryItem.style.transform = 'scale(1)';
                categoryItem.classList.remove('dragging-pulse');
                
                if (state.draggingCategoryId && state.draggingCategoryId !== categoryId) {
                    const draggingCategory = state.hiddenData.categories.find(c => c.id === state.draggingCategoryId);
                    const targetCategory = state.hiddenData.categories.find(c => c.id === categoryId);
                    
                    if (draggingCategory && targetCategory) {
                        const tempOrder = draggingCategory.order;
                        draggingCategory.order = targetCategory.order;
                        targetCategory.order = tempOrder;
                        
                        saveHiddenData();
                        renderHiddenCategories();
                    }
                }
            });
            
            categoryItem.addEventListener('dragend', (e) => {
                categoryItem.classList.remove('dragging');
                categoryItem.classList.remove('dragging-pulse');
                elements.hiddenCategoriesContainer.querySelectorAll('.category-item').forEach(item => {
                    item.style.border = 'none';
                    item.style.transform = 'scale(1)';
                });
                state.draggingCategoryId = null;
            });
        }

        // 渲染书签
        async function renderBookmarks() {
            elements.bookmarksContainer.innerHTML = '';
            
            const sortedCategories = [...state.categories].sort((a, b) => a.order - b.order);
            
            for (const category of sortedCategories) {
                const section = document.createElement('div');
                section.className = 'bookmarks-section';
                section.id = `category-${category.id}`;
                
                if (category.id === state.currentCategory) {
                    section.classList.add('active');
                    section.style.display = 'block';
                } else {
                    section.style.display = 'none';
                }
                
                const grid = document.createElement('div');
                grid.className = 'bookmarks-grid';
                
                const categoryBookmarks = state.bookmarks
                    .filter(bookmark => bookmark.categoryId === category.id)
                    .sort((a, b) => a.order - b.order);
                
                const rows = state.settings.rowsPerCategory || 4;
                const totalSlots = rows * 6;
                
                for (const bookmark of categoryBookmarks) {
                    const bookmarkElement = await createBookmarkElement(bookmark, category.id);
                    grid.appendChild(bookmarkElement);
                }
                
                // 添加空位（仅在编辑模式下显示）
                const emptySlots = totalSlots - categoryBookmarks.length;
                for (let i = 0; i < emptySlots; i++) {
                    const emptySlot = document.createElement('div');
                    emptySlot.className = 'bookmark-item empty-slot';
                    emptySlot.innerHTML = `
                        <div class="bookmark-icon"><i class="fas fa-plus"></i></div>
                        <div class="bookmark-name">空位</div>
                    `;
                    
                    if (state.editMode) {
                        emptySlot.style.opacity = '0.5';
                        emptySlot.style.cursor = 'pointer';
                        emptySlot.style.visibility = 'visible';
                        emptySlot.addEventListener('click', () => {
                            openAddBookmarkModal(category.id);
                        });
                    }
                    
                    grid.appendChild(emptySlot);
                }
                
                if (state.editMode) {
                    const addRowBtn = document.createElement('button');
                    addRowBtn.className = 'add-row-btn';
                    addRowBtn.innerHTML = '<i class="fas fa-plus-circle"></i> 增加一行 (6个位置)';
                    addRowBtn.addEventListener('click', () => {
                        openRowsApplyModal('add');
                    });
                    grid.appendChild(addRowBtn);
                    
                    if (rows > 1) {
                        const removeRowBtn = document.createElement('button');
                        removeRowBtn.className = 'remove-row-btn';
                        removeRowBtn.innerHTML = '<i class="fas fa-minus-circle"></i> 减少一行';
                        removeRowBtn.addEventListener('click', () => {
                            openRowsApplyModal('remove');
                        });
                        grid.appendChild(removeRowBtn);
                    }
                }
                
                section.appendChild(grid);
                elements.bookmarksContainer.appendChild(section);
            }
        }

        async function renderHiddenBookmarks() {
            elements.hiddenBookmarksContainer.innerHTML = '';
            
            const sortedCategories = [...state.hiddenData.categories].sort((a, b) => a.order - b.order);
            
            for (const category of sortedCategories) {
                const section = document.createElement('div');
                section.className = 'bookmarks-section';
                section.id = `hidden-category-${category.id}`;
                
                if (category.id === state.hiddenData.currentCategory) {
                    section.classList.add('active');
                    section.style.display = 'block';
                } else {
                    section.style.display = 'none';
                }
                
                const grid = document.createElement('div');
                grid.className = 'bookmarks-grid';
                
                const categoryBookmarks = state.hiddenData.bookmarks
                    .filter(bookmark => bookmark.categoryId === category.id)
                    .sort((a, b) => a.order - b.order);
                
                const rows = state.hiddenData.settings.rowsPerCategory || 4;
                const totalSlots = rows * 6;
                
                for (const bookmark of categoryBookmarks) {
                    const bookmarkElement = await createHiddenBookmarkElement(bookmark, category.id);
                    grid.appendChild(bookmarkElement);
                }
                
                // 添加空位（仅在编辑模式下显示）
                const emptySlots = totalSlots - categoryBookmarks.length;
                for (let i = 0; i < emptySlots; i++) {
                    const emptySlot = document.createElement('div');
                    emptySlot.className = 'bookmark-item empty-slot';
                    emptySlot.innerHTML = `
                        <div class="bookmark-icon"><i class="fas fa-plus"></i></div>
                        <div class="bookmark-name">空位</div>
                    `;
                    
                    if (state.editMode && state.isHiddenPage) {
                        emptySlot.style.opacity = '0.5';
                        emptySlot.style.cursor = 'pointer';
                        emptySlot.style.visibility = 'visible';
                        emptySlot.addEventListener('click', () => {
                            openHiddenAddBookmarkModal(category.id);
                        });
                    }
                    
                    grid.appendChild(emptySlot);
                }
                
                if (state.editMode && state.isHiddenPage) {
                    const addRowBtn = document.createElement('button');
                    addRowBtn.className = 'add-row-btn';
                    addRowBtn.innerHTML = '<i class="fas fa-plus-circle"></i> 增加一行 (6个位置)';
                    addRowBtn.addEventListener('click', () => {
                        openRowsApplyModal('add');
                    });
                    grid.appendChild(addRowBtn);
                    
                    if (rows > 1) {
                        const removeRowBtn = document.createElement('button');
                        removeRowBtn.className = 'remove-row-btn';
                        removeRowBtn.innerHTML = '<i class="fas fa-minus-circle"></i> 减少一行';
                        removeRowBtn.addEventListener('click', () => {
                            openRowsApplyModal('remove');
                        });
                        grid.appendChild(removeRowBtn);
                    }
                }
                
                section.appendChild(grid);
                elements.hiddenBookmarksContainer.appendChild(section);
            }
        }

        // 创建书签元素
        async function createBookmarkElement(bookmark, categoryId) {
            const item = document.createElement('a');
            item.className = 'bookmark-item';
            item.href = bookmark.url;
            item.target = '_blank';
            item.dataset.id = bookmark.id;
            item.dataset.category = categoryId;
            item.dataset.order = bookmark.order;
            
            let iconHTML;
            if (bookmark.customIcon) {
                iconHTML = `<i class="${bookmark.customIcon}"></i>`;
            } else {
                const faviconUrl = await getFavicon(bookmark.url);
                if (faviconUrl) {
                    iconHTML = `<img class="bookmark-icon-img" src="${faviconUrl}" alt="${bookmark.name}图标" onerror="handleFaviconError(this, ${bookmark.id})">`;
                } else {
                    const icon = getIconByWebsiteType(bookmark.name, bookmark.url);
                    iconHTML = `<i class="${icon}"></i>`;
                    bookmark.customIcon = icon;
                    saveData();
                }
            }
            
            // 限制名称长度（最多8个字符）
            const displayName = bookmark.name.length > 8 ? bookmark.name.substring(0, 8) : bookmark.name;
            
            item.innerHTML = `
                <div class="bookmark-icon">${iconHTML}</div>
                <div class="bookmark-name" title="${bookmark.name}">${displayName}</div>
                <button class="bookmark-edit-btn" data-id="${bookmark.id}">
                    <i class="fas fa-edit"></i>
                </button>
            `;
            
            const editBtn = item.querySelector('.bookmark-edit-btn');
            editBtn.addEventListener('click', (e) => {
                e.preventDefault();
                e.stopPropagation();
                openEditBookmarkModal(bookmark.id);
            });
            
            if (state.editMode) {
                item.draggable = true;
                item.addEventListener('click', (e) => {
                    e.preventDefault();
                });
                
                // 拖拽事件监听器
                setupBookmarkDragEvents(item, bookmark.id);
            }
            
            return item;
        }

        async function createHiddenBookmarkElement(bookmark, categoryId) {
            const item = document.createElement('a');
            item.className = 'bookmark-item';
            item.href = bookmark.url;
            item.target = '_blank';
            item.dataset.id = bookmark.id;
            item.dataset.category = categoryId;
            item.dataset.order = bookmark.order;
            
            let iconHTML;
            if (bookmark.customIcon) {
                iconHTML = `<i class="${bookmark.customIcon}"></i>`;
            } else {
                const faviconUrl = await getFavicon(bookmark.url);
                if (faviconUrl) {
                    iconHTML = `<img class="bookmark-icon-img" src="${faviconUrl}" alt="${bookmark.name}图标" onerror="handleHiddenFaviconError(this, ${bookmark.id})">`;
                } else {
                    const icon = getIconByWebsiteType(bookmark.name, bookmark.url);
                    iconHTML = `<i class="${icon}"></i>`;
                    bookmark.customIcon = icon;
                    saveHiddenData();
                }
            }
            
            // 限制名称长度（最多8个字符）
            const displayName = bookmark.name.length > 8 ? bookmark.name.substring(0, 8) : bookmark.name;
            
            item.innerHTML = `
                <div class="bookmark-icon">${iconHTML}</div>
                <div class="bookmark-name" title="${bookmark.name}">${displayName}</div>
                <button class="bookmark-edit-btn" data-id="${bookmark.id}">
                    <i class="fas fa-edit"></i>
                </button>
            `;
            
            const editBtn = item.querySelector('.bookmark-edit-btn');
            editBtn.addEventListener('click', (e) => {
                e.preventDefault();
                e.stopPropagation();
                openHiddenEditBookmarkModal(bookmark.id);
            });
            
            if (state.editMode && state.isHiddenPage) {
                item.draggable = true;
                item.addEventListener('click', (e) => {
                    e.preventDefault();
                });
                
                // 拖拽事件监听器
                setupHiddenBookmarkDragEvents(item, bookmark.id);
            }
            
            return item;
        }

        // 设置书签拖拽事件
        function setupBookmarkDragEvents(item, bookmarkId) {
            item.addEventListener('dragstart', (e) => {
                state.draggingBookmarkId = bookmarkId;
                item.classList.add('dragging');
                e.dataTransfer.setData('text/plain', bookmarkId);
                e.dataTransfer.effectAllowed = 'move';
            });
            
            item.addEventListener('dragover', (e) => {
                e.preventDefault();
                e.dataTransfer.dropEffect = 'move';
                item.classList.add('dragging-pulse');
            });
            
            item.addEventListener('dragenter', (e) => {
                if (state.draggingBookmarkId !== bookmarkId) {
                    item.style.border = '2px dashed rgba(255, 255, 255, 0.5)';
                    item.style.transform = 'scale(1.05)';
                }
            });
            
            item.addEventListener('dragleave', (e) => {
                item.style.border = 'none';
                item.style.transform = 'none';
                item.classList.remove('dragging-pulse');
            });
            
            item.addEventListener('drop', (e) => {
                e.preventDefault();
                item.style.border = 'none';
                item.style.transform = 'none';
                item.classList.remove('dragging-pulse');
                
                if (state.draggingBookmarkId && state.draggingBookmarkId !== bookmarkId) {
                    const draggingBookmark = state.bookmarks.find(b => b.id === state.draggingBookmarkId);
                    const targetBookmark = state.bookmarks.find(b => b.id === bookmarkId);
                    
                    if (draggingBookmark && targetBookmark && draggingBookmark.categoryId === targetBookmark.categoryId) {
                        const tempOrder = draggingBookmark.order;
                        draggingBookmark.order = targetBookmark.order;
                        targetBookmark.order = tempOrder;
                        
                        saveData();
                        renderBookmarks();
                    }
                }
            });
            
            item.addEventListener('dragend', (e) => {
                item.classList.remove('dragging');
                item.classList.remove('dragging-pulse');
                document.querySelectorAll('.bookmark-item').forEach(item => {
                    item.style.border = 'none';
                    item.style.transform = 'none';
                });
                state.draggingBookmarkId = null;
            });
        }

        function setupHiddenBookmarkDragEvents(item, bookmarkId) {
            item.addEventListener('dragstart', (e) => {
                state.draggingBookmarkId = bookmarkId;
                item.classList.add('dragging');
                e.dataTransfer.setData('text/plain', bookmarkId);
                e.dataTransfer.effectAllowed = 'move';
            });
            
            item.addEventListener('dragover', (e) => {
                e.preventDefault();
                e.dataTransfer.dropEffect = 'move';
                item.classList.add('dragging-pulse');
            });
            
            item.addEventListener('dragenter', (e) => {
                if (state.draggingBookmarkId !== bookmarkId) {
                    item.style.border = '2px dashed rgba(255, 255, 255, 0.5)';
                    item.style.transform = 'scale(1.05)';
                }
            });
            
            item.addEventListener('dragleave', (e) => {
                item.style.border = 'none';
                item.style.transform = 'none';
                item.classList.remove('dragging-pulse');
            });
            
            item.addEventListener('drop', (e) => {
                e.preventDefault();
                item.style.border = 'none';
                item.style.transform = 'none';
                item.classList.remove('dragging-pulse');
                
                if (state.draggingBookmarkId && state.draggingBookmarkId !== bookmarkId) {
                    const draggingBookmark = state.hiddenData.bookmarks.find(b => b.id === state.draggingBookmarkId);
                    const targetBookmark = state.hiddenData.bookmarks.find(b => b.id === bookmarkId);
                    
                    if (draggingBookmark && targetBookmark && draggingBookmark.categoryId === targetBookmark.categoryId) {
                        const tempOrder = draggingBookmark.order;
                        draggingBookmark.order = targetBookmark.order;
                        targetBookmark.order = tempOrder;
                        
                        saveHiddenData();
                        renderHiddenBookmarks();
                    }
                }
            });
            
            item.addEventListener('dragend', (e) => {
                item.classList.remove('dragging');
                item.classList.remove('dragging-pulse');
                elements.hiddenBookmarksContainer.querySelectorAll('.bookmark-item').forEach(item => {
                    item.style.border = 'none';
                    item.style.transform = 'none';
                });
                state.draggingBookmarkId = null;
            });
        }

        // 根据网站类型获取图标
        function getIconByWebsiteType(name, url) {
            const nameLower = name.toLowerCase();
            const urlLower = url.toLowerCase();
            
            if (nameLower.includes('搜索') || nameLower.includes('google') || nameLower.includes('百度') || nameLower.includes('bing')) {
                return 'fas fa-search icon-search';
            }
            else if (nameLower.includes('视频') || nameLower.includes('youtube') || nameLower.includes('bilibili') || nameLower.includes('优酷') || nameLower.includes('爱奇艺')) {
                return 'fas fa-film icon-video';
            }
            else if (nameLower.includes('社交') || nameLower.includes('微信') || nameLower.includes('微博') || nameLower.includes('facebook') || nameLower.includes('twitter')) {
                return 'fab fa-weixin icon-social';
            }
            else if (nameLower.includes('购物') || nameLower.includes('淘宝') || nameLower.includes('京东') || nameLower.includes('amazon') || nameLower.includes('shop')) {
                return 'fas fa-shopping-cart icon-shopping';
            }
            else if (nameLower.includes('旅行') || nameLower.includes('机票') || nameLower.includes('酒店') || nameLower.includes('携程') || nameLower.includes('trip')) {
                return 'fas fa-plane icon-travel';
            }
            else if (nameLower.includes('工具') || nameLower.includes('工具') || nameLower.includes('utility') || nameLower.includes('tool')) {
                return 'fas fa-wrench icon-tools';
            }
            else if (nameLower.includes('新闻') || nameLower.includes('news') || nameLower.includes('媒体')) {
                return 'fas fa-newspaper icon-news';
            }
            else if (nameLower.includes('音乐') || nameLower.includes('music') || nameLower.includes('网易云')) {
                return 'fas fa-music icon-music';
            }
            else if (nameLower.includes('游戏') || nameLower.includes('game') || nameLower.includes('play')) {
                return 'fas fa-gamepad icon-games';
            }
            else if (nameLower.includes('工作') || nameLower.includes('企业') || nameLower.includes('office') || nameLower.includes('工作')) {
                return 'fas fa-briefcase icon-work';
            }
            else {
                const randomIndex = Math.floor(Math.random() * state.defaultIcons.length);
                return state.defaultIcons[randomIndex].class;
            }
        }

        // favicon加载错误处理
        function handleFaviconError(imgElement, bookmarkId) {
            const bookmark = state.bookmarks.find(b => b.id === bookmarkId);
            if (bookmark) {
                const icon = getIconByWebsiteType(bookmark.name, bookmark.url);
                imgElement.style.display = 'none';
                imgElement.parentElement.innerHTML = `<i class="${icon}"></i>`;
                bookmark.customIcon = icon;
                saveData();
            }
        }

        function handleHiddenFaviconError(imgElement, bookmarkId) {
            const bookmark = state.hiddenData.bookmarks.find(b => b.id === bookmarkId);
            if (bookmark) {
                const icon = getIconByWebsiteType(bookmark.name, bookmark.url);
                imgElement.style.display = 'none';
                imgElement.parentElement.innerHTML = `<i class="${icon}"></i>`;
                bookmark.customIcon = icon;
                saveHiddenData();
            }
        }

        // 设置活动分类
        function setActiveCategory(categoryId, initialLoad = false) {
            state.currentCategory = categoryId;
            
            document.querySelectorAll('.category-btn').forEach(btn => {
                if (parseInt(btn.dataset.id) === categoryId) {
                    btn.classList.add('active');
                } else {
                    btn.classList.remove('active');
                }
            });
            
            document.querySelectorAll('.bookmarks-section').forEach(section => {
                if (section.id === `category-${categoryId}`) {
                    section.classList.add('active');
                    section.style.display = 'block';
                } else {
                    section.classList.remove('active');
                    section.style.display = 'none';
                }
            });
        }

        function setHiddenActiveCategory(categoryId, initialLoad = false) {
            state.hiddenData.currentCategory = categoryId;
            
            elements.hiddenCategoriesContainer.querySelectorAll('.category-btn').forEach(btn => {
                if (parseInt(btn.dataset.id) === categoryId) {
                    btn.classList.add('active');
                } else {
                    btn.classList.remove('active');
                }
            });
            
            elements.hiddenBookmarksContainer.querySelectorAll('.bookmarks-section').forEach(section => {
                if (section.id === `hidden-category-${categoryId}`) {
                    section.classList.add('active');
                    section.style.display = 'block';
                } else {
                    section.classList.remove('active');
                    section.style.display = 'none';
                }
            });
        }

        // 应用设置
        function applySettings() {
            const settings = state.settings;
            
            if (settings.backgroundType === 'gradient') {
                document.body.style.background = settings.backgroundValue;
                elements.backgroundImage.style.display = 'none';
                document.body.classList.remove('no-texture');
            } else if (settings.backgroundType === 'image') {
                document.body.style.background = '';
                elements.backgroundImage.src = settings.backgroundValue;
                elements.backgroundImage.style.display = 'block';
                document.body.classList.add('no-texture');
            }
            
            document.documentElement.style.setProperty('--primary-color', settings.primaryColor);
            document.documentElement.style.setProperty('--secondary-color', settings.secondaryColor);
            document.documentElement.style.setProperty('--bg-color', settings.backgroundValue);
            document.documentElement.style.setProperty('--text-color', settings.textColor);
            document.documentElement.style.setProperty('--category-color', settings.categoryColor);
            document.documentElement.style.setProperty('--bookmark-color', settings.bookmarkColor);
            document.documentElement.style.setProperty('--title-font', settings.pageTitleFont);
            document.documentElement.style.setProperty('--subtitle-font', settings.pageSubtitleFont);
            
            if (settings.pageTitle) {
                elements.pageTitle.textContent = settings.pageTitle;
                elements.pageTitle.style.fontSize = settings.pageTitleFontSize;
                elements.pageTitle.style.fontFamily = settings.pageTitleFont;
                
                if (settings.pageTitleIcon) {
                    const existingIcon = elements.pageTitle.querySelector('.page-title-icon');
                    if (existingIcon) {
                        existingIcon.remove();
                    }
                    
                    const icon = document.createElement('img');
                    icon.className = 'page-title-icon';
                    icon.src = settings.pageTitleIcon;
                    icon.alt = '标题图标';
                    elements.pageTitle.prepend(icon);
                    
                    const fontSize = parseInt(settings.pageTitleFontSize);
                    icon.style.width = `${fontSize * 1.2}px`;
                    icon.style.height = `${fontSize * 1.2}px`;
                } else {
                    const existingIcon = elements.pageTitle.querySelector('.page-title-icon');
                    if (existingIcon) {
                        existingIcon.remove();
                    }
                }
            } else {
                elements.pageTitle.textContent = '';
            }
            
            if (settings.pageSubtitle) {
                elements.pageSubtitle.textContent = settings.pageSubtitle;
                elements.pageSubtitle.style.fontFamily = settings.pageSubtitleFont;
            } else {
                elements.pageSubtitle.textContent = '';
            }
        }

        function applyHiddenSettings() {
            const settings = state.hiddenData.settings;
            
            if (settings.pageTitle) {
                elements.hiddenPageTitle.textContent = settings.pageTitle;
                elements.hiddenPageTitle.style.fontSize = settings.pageTitleFontSize;
                elements.hiddenPageTitle.style.fontFamily = settings.pageTitleFont;
                
                if (settings.pageTitleIcon) {
                    const existingIcon = elements.hiddenPageTitle.querySelector('.page-title-icon');
                    if (existingIcon) {
                        existingIcon.remove();
                    }
                    
                    const icon = document.createElement('img');
                    icon.className = 'page-title-icon';
                    icon.src = settings.pageTitleIcon;
                    icon.alt = '标题图标';
                    elements.hiddenPageTitle.prepend(icon);
                    
                    const fontSize = parseInt(settings.pageTitleFontSize);
                    icon.style.width = `${fontSize * 1.2}px`;
                    icon.style.height = `${fontSize * 1.2}px`;
                } else {
                    const existingIcon = elements.hiddenPageTitle.querySelector('.page-title-icon');
                    if (existingIcon) {
                        existingIcon.remove();
                    }
                }
            } else {
                elements.hiddenPageTitle.textContent = '';
            }
            
            if (settings.pageSubtitle) {
                elements.hiddenPageSubtitle.textContent = settings.pageSubtitle;
                elements.hiddenPageSubtitle.style.fontFamily = settings.pageSubtitleFont;
            } else {
                elements.hiddenPageSubtitle.textContent = '';
            }
        }

        // 更新搜索引擎显示
        function updateSearchEngineDisplay() {
            const engine = state.searchEngines[state.settings.searchEngine];
            if (engine) {
                elements.currentEngine.innerHTML = `
                    <i class="${engine.icon}"></i>
                    <span class="engine-name" style="display: none;">${engine.name}</span>
                `;
                elements.currentEngine.title = engine.name;
            }
        }

        function updateHiddenSearchEngineDisplay() {
            const engine = state.searchEngines[state.hiddenData.settings.searchEngine];
            if (engine) {
                elements.hiddenCurrentEngine.innerHTML = `
                    <i class="${engine.icon}"></i>
                    <span class="engine-name" style="display: none;">${engine.name}</span>
                `;
                elements.hiddenCurrentEngine.title = engine.name;
            }
        }

        // 更新搜索功能状态
        function updateSearchFunctionState() {
            if (state.editMode) {
                elements.searchInput.classList.add('disabled');
                elements.searchInput.disabled = true;
                elements.searchBtn.classList.add('disabled');
                elements.currentEngine.style.opacity = '0.5';
                elements.currentEngine.style.cursor = 'not-allowed';
                elements.currentEngine.style.pointerEvents = 'none';
                
                if (state.isHiddenPage) {
                    elements.hiddenSearchInput.classList.add('disabled');
                    elements.hiddenSearchInput.disabled = true;
                    elements.hiddenSearchBtn.classList.add('disabled');
                    elements.hiddenCurrentEngine.style.opacity = '0.5';
                    elements.hiddenCurrentEngine.style.cursor = 'not-allowed';
                    elements.hiddenCurrentEngine.style.pointerEvents = 'none';
                }
            } else {
                elements.searchInput.classList.remove('disabled');
                elements.searchInput.disabled = false;
                elements.searchBtn.classList.remove('disabled');
                elements.currentEngine.style.opacity = '1';
                elements.currentEngine.style.cursor = 'pointer';
                elements.currentEngine.style.pointerEvents = 'auto';
                
                if (state.isHiddenPage) {
                    elements.hiddenSearchInput.classList.remove('disabled');
                    elements.hiddenSearchInput.disabled = false;
                    elements.hiddenSearchBtn.classList.remove('disabled');
                    elements.hiddenCurrentEngine.style.opacity = '1';
                    elements.hiddenCurrentEngine.style.cursor = 'pointer';
                    elements.hiddenCurrentEngine.style.pointerEvents = 'auto';
                }
            }
        }

        // 打开添加网站模态框
        function openAddBookmarkModal(categoryId) {
            state.editingBookmarkId = null;
            document.getElementById('editBookmarkName').value = '';
            document.getElementById('editBookmarkUrl').value = '';
            
            document.querySelectorAll('.icon-option').forEach(option => {
                option.classList.remove('selected');
            });
            
            document.getElementById('editBookmarkForm').dataset.categoryId = categoryId;
            
            elements.editBookmarkModal.style.display = 'flex';
        }

        function openHiddenAddBookmarkModal(categoryId) {
            state.editingBookmarkId = null;
            document.getElementById('editBookmarkName').value = '';
            document.getElementById('editBookmarkUrl').value = '';
            
            document.querySelectorAll('.icon-option').forEach(option => {
                option.classList.remove('selected');
            });
            
            document.getElementById('editBookmarkForm').dataset.categoryId = categoryId;
            document.getElementById('editBookmarkForm').dataset.hidden = 'true';
            
            elements.editBookmarkModal.style.display = 'flex';
        }

        // 打开编辑网站模态框
        function openEditBookmarkModal(bookmarkId) {
            const bookmark = state.bookmarks.find(b => b.id === bookmarkId);
            if (!bookmark) return;
            
            state.editingBookmarkId = bookmarkId;
            document.getElementById('editBookmarkName').value = bookmark.name;
            document.getElementById('editBookmarkUrl').value = bookmark.url;
            
            document.querySelectorAll('.icon-option').forEach(option => {
                option.classList.remove('selected');
            });
            
            if (bookmark.customIcon) {
                const iconOption = document.querySelector(`.icon-option[data-icon="${bookmark.customIcon}"]`);
                if (iconOption) {
                    iconOption.classList.add('selected');
                }
            }
            
            document.getElementById('editBookmarkForm').dataset.hidden = 'false';
            
            elements.editBookmarkModal.style.display = 'flex';
        }

        function openHiddenEditBookmarkModal(bookmarkId) {
            const bookmark = state.hiddenData.bookmarks.find(b => b.id === bookmarkId);
            if (!bookmark) return;
            
            state.editingBookmarkId = bookmarkId;
            document.getElementById('editBookmarkName').value = bookmark.name;
            document.getElementById('editBookmarkUrl').value = bookmark.url;
            
            document.querySelectorAll('.icon-option').forEach(option => {
                option.classList.remove('selected');
            });
            
            if (bookmark.customIcon) {
                const iconOption = document.querySelector(`.icon-option[data-icon="${bookmark.customIcon}"]`);
                if (iconOption) {
                    iconOption.classList.add('selected');
                }
            }
            
            document.getElementById('editBookmarkForm').dataset.hidden = 'true';
            
            elements.editBookmarkModal.style.display = 'flex';
        }

        // 保存网站
        async function saveBookmark(e) {
            e.preventDefault();
            
            const name = document.getElementById('editBookmarkName').value.trim();
            const url = document.getElementById('editBookmarkUrl').value.trim();
            const isHidden = document.getElementById('editBookmarkForm').dataset.hidden === 'true';
            
            if (!name || !url) {
                alert('请填写所有必填字段');
                return;
            }
            
            let finalUrl = url;
            if (!url.startsWith('http://') && !url.startsWith('https://')) {
                finalUrl = 'https://' + url;
            }
            
            try {
                new URL(finalUrl);
            } catch (error) {
                alert('请输入有效的URL地址，例如：https://www.example.com');
                return;
            }
            
            const selectedIcon = document.querySelector('.icon-option.selected');
            const customIcon = selectedIcon ? selectedIcon.dataset.icon : null;
            
            if (state.editingBookmarkId) {
                if (isHidden) {
                    const index = state.hiddenData.bookmarks.findIndex(b => b.id === state.editingBookmarkId);
                    if (index !== -1) {
                        state.hiddenData.bookmarks[index] = {
                            ...state.hiddenData.bookmarks[index],
                            name,
                            url: finalUrl,
                            customIcon
                        };
                    }
                } else {
                    const index = state.bookmarks.findIndex(b => b.id === state.editingBookmarkId);
                    if (index !== -1) {
                        state.bookmarks[index] = {
                            ...state.bookmarks[index],
                            name,
                            url: finalUrl,
                            customIcon
                        };
                        delete state.faviconCache[state.bookmarks[index].url];
                    }
                }
            } else {
                const categoryId = parseInt(document.getElementById('editBookmarkForm').dataset.categoryId);
                
                if (isHidden) {
                    const categoryBookmarks = state.hiddenData.bookmarks.filter(b => b.categoryId === categoryId);
                    const maxOrder = categoryBookmarks.length > 0 ? Math.max(...categoryBookmarks.map(b => b.order)) : 0;
                    
                    const newId = state.hiddenData.bookmarks.length > 0 ? Math.max(...state.hiddenData.bookmarks.map(b => b.id)) + 1 : 1;
                    state.hiddenData.bookmarks.push({
                        id: newId,
                        name,
                        url: finalUrl,
                        categoryId,
                        order: maxOrder + 1,
                        customIcon
                    });
                } else {
                    const categoryBookmarks = state.bookmarks.filter(b => b.categoryId === categoryId);
                    const maxOrder = categoryBookmarks.length > 0 ? Math.max(...categoryBookmarks.map(b => b.order)) : 0;
                    
                    const newId = state.bookmarks.length > 0 ? Math.max(...state.bookmarks.map(b => b.id)) + 1 : 1;
                    state.bookmarks.push({
                        id: newId,
                        name,
                        url: finalUrl,
                        categoryId,
                        order: maxOrder + 1,
                        customIcon
                    });
                }
            }
            
            await getFavicon(finalUrl);
            
            if (isHidden) {
                saveHiddenData();
                renderHiddenBookmarks();
            } else {
                saveData();
                renderBookmarks();
            }
            
            closeModal(elements.editBookmarkModal);
        }

        // 打开添加分类模态框
        function openAddCategoryModal() {
            document.getElementById('addCategoryName').value = '';
            elements.addCategoryModal.style.display = 'flex';
        }

        function openHiddenAddCategoryModal() {
            document.getElementById('addCategoryName').value = '';
            document.getElementById('addCategoryForm').dataset.hidden = 'true';
            elements.addCategoryModal.style.display = 'flex';
        }

        // 保存添加的分类
        function saveAddCategory(e) {
            e.preventDefault();
            
            const name = document.getElementById('addCategoryName').value.trim();
            const isHidden = document.getElementById('addCategoryForm').dataset.hidden === 'true';
            
            if (!name) {
                alert('请输入分类名称');
                return;
            }
            
            if (isHidden) {
                if (state.hiddenData.categories.some(c => c.name === name)) {
                    alert('分类名称已存在');
                    return;
                }
                
                const maxOrder = state.hiddenData.categories.length > 0 ? Math.max(...state.hiddenData.categories.map(c => c.order)) : 0;
                const newId = state.hiddenData.categories.length > 0 ? Math.max(...state.hiddenData.categories.map(c => c.id)) + 1 : 1;
                state.hiddenData.categories.push({
                    id: newId,
                    name,
                    order: maxOrder + 1
                });
                
                saveHiddenData();
                renderHiddenCategories();
                setHiddenActiveCategory(newId);
                renderHiddenBookmarks();
            } else {
                if (state.categories.some(c => c.name === name)) {
                    alert('分类名称已存在');
                    return;
                }
                
                const maxOrder = state.categories.length > 0 ? Math.max(...state.categories.map(c => c.order)) : 0;
                const newId = state.categories.length > 0 ? Math.max(...state.categories.map(c => c.id)) + 1 : 1;
                state.categories.push({
                    id: newId,
                    name,
                    order: maxOrder + 1
                });
                
                saveData();
                renderCategories();
                setActiveCategory(newId);
                renderBookmarks();
            }
            
            closeModal(elements.addCategoryModal);
        }

        // 打开编辑分类模态框
        function openEditCategoryModal(categoryId) {
            const category = state.categories.find(c => c.id === categoryId);
            if (!category) return;
            
            state.editingCategoryId = categoryId;
            document.getElementById('editCategoryName').value = category.name;
            document.getElementById('editCategoryForm').dataset.hidden = 'false';
            
            elements.editCategoryModal.style.display = 'flex';
        }

        function openHiddenEditCategoryModal(categoryId) {
            const category = state.hiddenData.categories.find(c => c.id === categoryId);
            if (!category) return;
            
            state.editingCategoryId = categoryId;
            document.getElementById('editCategoryName').value = category.name;
            document.getElementById('editCategoryForm').dataset.hidden = 'true';
            
            elements.editCategoryModal.style.display = 'flex';
        }

        // 保存分类编辑
        function saveCategory(e) {
            e.preventDefault();
            
            const name = document.getElementById('editCategoryName').value.trim();
            const isHidden = document.getElementById('editCategoryForm').dataset.hidden === 'true';
            
            if (!name) {
                alert('请输入分类名称');
                return;
            }
            
            if (isHidden) {
                if (state.hiddenData.categories.some(c => c.name === name && c.id !== state.editingCategoryId)) {
                    alert('分类名称已存在');
                    return;
                }
                
                const index = state.hiddenData.categories.findIndex(c => c.id === state.editingCategoryId);
                if (index !== -1) {
                    state.hiddenData.categories[index].name = name;
                }
                
                saveHiddenData();
                renderHiddenCategories();
            } else {
                if (state.categories.some(c => c.name === name && c.id !== state.editingCategoryId)) {
                    alert('分类名称已存在');
                    return;
                }
                
                const index = state.categories.findIndex(c => c.id === state.editingCategoryId);
                if (index !== -1) {
                    state.categories[index].name = name;
                }
                
                saveData();
                renderCategories();
            }
            
            closeModal(elements.editCategoryModal);
        }

        // 删除分类
        function deleteCategory(categoryId) {
            if (state.categories.length <= 1) {
                alert('至少需要保留一个分类');
                return;
            }
            
            if (!confirm('确定要删除这个分类吗？分类下的所有网站也将被删除。')) {
                return;
            }
            
            state.categories = state.categories.filter(c => c.id !== categoryId);
            state.bookmarks = state.bookmarks.filter(b => b.categoryId !== categoryId);
            
            if (state.currentCategory === categoryId) {
                state.currentCategory = state.categories[0].id;
            }
            
            ensureOrderFields();
            
            saveData();
            renderCategories();
            renderBookmarks();
            setActiveCategory(state.currentCategory);
        }

        function deleteHiddenCategory(categoryId) {
            if (state.hiddenData.categories.length <= 1) {
                alert('至少需要保留一个分类');
                return;
            }
            
            if (!confirm('确定要删除这个分类吗？分类下的所有网站也将被删除。')) {
                return;
            }
            
            state.hiddenData.categories = state.hiddenData.categories.filter(c => c.id !== categoryId);
            state.hiddenData.bookmarks = state.hiddenData.bookmarks.filter(b => b.categoryId !== categoryId);
            
            if (state.hiddenData.currentCategory === categoryId) {
                state.hiddenData.currentCategory = state.hiddenData.categories[0].id;
            }
            
            ensureHiddenOrderFields();
            
            saveHiddenData();
            renderHiddenCategories();
            renderHiddenBookmarks();
            setHiddenActiveCategory(state.hiddenData.currentCategory);
        }

        // 打开配色和背景模态框
        function openColorBgModal() {
            // 重置选择
            state.selectedSkin = null;
            document.querySelectorAll('.skin-item').forEach(item => {
                item.classList.remove('selected');
            });
            
            // 设置当前值到颜色选择器
            document.getElementById('titleColorPicker').value = state.settings.textColor;
            document.getElementById('titleColorValue').textContent = state.settings.textColor.toUpperCase();
            document.getElementById('categoryColorPicker').value = state.settings.categoryColor;
            document.getElementById('categoryColorValue').textContent = state.settings.categoryColor.toUpperCase();
            document.getElementById('bookmarkColorPicker').value = state.settings.bookmarkColor;
            document.getElementById('bookmarkColorValue').textContent = state.settings.bookmarkColor.toUpperCase();
            document.getElementById('primaryColorPicker').value = state.settings.primaryColor;
            document.getElementById('primaryColorValue').textContent = state.settings.primaryColor.toUpperCase();
            document.getElementById('secondaryColorPicker').value = state.settings.secondaryColor;
            document.getElementById('secondaryColorValue').textContent = state.settings.secondaryColor.toUpperCase();
            
            // 重置背景选择
            document.querySelectorAll('.bg-option').forEach(option => {
                option.classList.remove('selected');
            });
            
            // 根据当前背景类型选择对应选项
            if (state.settings.backgroundType === 'gradient') {
                const gradientMap = {
                    'linear-gradient(135deg, #667eea 0%, #764ba2 100%)': 'gradient1',
                    'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)': 'gradient2',
                    'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)': 'gradient3',
                    'linear-gradient(135deg, #43e97b 0%, #38f9d7 100%)': 'gradient4',
                    'linear-gradient(135deg, #fa709a 0%, #fee140 100%)': 'gradient5'
                };
                
                const currentBg = gradientMap[state.settings.backgroundValue];
                if (currentBg) {
                    const option = document.getElementById(currentBg);
                    if (option) option.classList.add('selected');
                }
            }
            
            // 设置标题文字
            document.getElementById('editTitleText').value = state.settings.pageTitle;
            document.getElementById('editSubtitleText').value = state.settings.pageSubtitle;
            
            // 设置标题图标
            if (state.settings.pageTitleIcon) {
                document.getElementById('titleIconPreview').src = state.settings.pageTitleIcon;
                document.getElementById('titleIconPreview').style.display = 'block';
            } else {
                document.getElementById('titleIconPreview').style.display = 'none';
            }
            
            // 设置字体大小
            const fontSize = parseInt(state.settings.pageTitleFontSize) || 48;
            document.getElementById('titleFontSize').value = fontSize;
            document.getElementById('fontSizeValue').textContent = fontSize + 'px';
            
            // 设置字体选择器
            document.querySelectorAll('#titleFontSelector .font-option').forEach(option => {
                option.classList.remove('selected');
                if (option.dataset.font === state.settings.pageTitleFont) {
                    option.classList.add('selected');
                }
            });
            
            document.querySelectorAll('#subtitleFontSelector .font-option').forEach(option => {
                option.classList.remove('selected');
                if (option.dataset.font === state.settings.pageSubtitleFont) {
                    option.classList.add('selected');
                }
            });
            
            elements.colorBgModal.style.display = 'flex';
            elements.settingsMenu.classList.remove('show');
        }

        // 打开管理行数模态框
        function openManageRowsModal() {
            const currentRows = state.isHiddenPage ? 
                state.hiddenData.settings.rowsPerCategory : 
                state.settings.rowsPerCategory;
            
            elements.currentRowsCount.textContent = currentRows;
            elements.rowsError.classList.remove('show');
            
            elements.manageRowsModal.style.display = 'flex';
            elements.settingsMenu.classList.remove('show');
        }

        // 打开行数应用选择模态框
        function openRowsApplyModal(action) {
            state.rowsChangeAction = action;
            elements.rowsApplyModal.style.display = 'flex';
        }

        // 应用皮肤
        function applySkin() {
            if (!state.selectedSkin) {
                alert('请选择一个皮肤');
                return;
            }
            
            // 应用皮肤设置
            state.settings.primaryColor = state.selectedSkin.primaryColor;
            state.settings.secondaryColor = state.selectedSkin.secondaryColor;
            state.settings.backgroundType = state.selectedSkin.bgType;
            state.settings.backgroundValue = state.selectedSkin.bgValue;
            state.settings.textColor = state.selectedSkin.textColor;
            state.settings.categoryColor = state.selectedSkin.categoryColor;
            state.settings.bookmarkColor = state.selectedSkin.bookmarkColor;
            
            saveData();
            applySettings();
            closeModal(elements.colorBgModal);
            
            alert('皮肤应用成功！');
        }

        // 应用颜色
        function applyColors() {
            const titleColor = document.getElementById('titleColorPicker').value;
            const categoryColor = document.getElementById('categoryColorPicker').value;
            const bookmarkColor = document.getElementById('bookmarkColorPicker').value;
            const primaryColor = document.getElementById('primaryColorPicker').value;
            const secondaryColor = document.getElementById('secondaryColorPicker').value;
            
            state.settings.textColor = titleColor;
            state.settings.categoryColor = categoryColor;
            state.settings.bookmarkColor = bookmarkColor;
            state.settings.primaryColor = primaryColor;
            state.settings.secondaryColor = secondaryColor;
            
            // 如果当前是渐变色背景，更新渐变
            if (state.settings.backgroundType === 'gradient') {
                state.settings.backgroundValue = `linear-gradient(135deg, ${primaryColor} 0%, ${secondaryColor} 100%)`;
            }
            
            saveData();
            applySettings();
            closeModal(elements.colorBgModal);
            
            alert('颜色应用成功！');
        }

        // 应用背景
        function applyBackground() {
            const selectedBg = document.querySelector('.bg-option.selected');
            if (!selectedBg && !document.getElementById('imageUploadInput').files[0]) {
                alert('请选择一个背景选项或上传图片');
                return;
            }
            
            if (selectedBg && selectedBg.id === 'imageUpload') {
                const fileInput = document.getElementById('imageUploadInput');
                if (fileInput.files && fileInput.files[0]) {
                    const file = fileInput.files[0];
                    
                    if (!file.type.startsWith('image/')) {
                        elements.imageError.textContent = '请选择图片文件';
                        elements.imageError.classList.add('show');
                        return;
                    }
                    
                    // 重置文件输入，允许选择同一文件
                    fileInput.value = '';
                    
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        state.settings.backgroundType = 'image';
                        state.settings.backgroundValue = e.target.result;
                        saveData();
                        applySettings();
                        closeModal(elements.colorBgModal);
                        alert('背景图片应用成功！');
                    };
                    reader.readAsDataURL(file);
                } else {
                    alert('请选择一张图片');
                }
            } else if (selectedBg) {
                const gradientMap = {
                    'gradient1': {
                        value: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
                        primary: '#667eea',
                        secondary: '#764ba2'
                    },
                    'gradient2': {
                        value: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
                        primary: '#f093fb',
                        secondary: '#f5576c'
                    },
                    'gradient3': {
                        value: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
                        primary: '#4facfe',
                        secondary: '#00f2fe'
                    },
                    'gradient4': {
                        value: 'linear-gradient(135deg, #43e97b 0%, #38f9d7 100%)',
                        primary: '#43e97b',
                        secondary: '#38f9d7'
                    },
                    'gradient5': {
                        value: 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)',
                        primary: '#fa709a',
                        secondary: '#fee140'
                    }
                };
                
                if (gradientMap[selectedBg.id]) {
                    state.settings.backgroundType = 'gradient';
                    state.settings.backgroundValue = gradientMap[selectedBg.id].value;
                    state.settings.primaryColor = gradientMap[selectedBg.id].primary;
                    state.settings.secondaryColor = gradientMap[selectedBg.id].secondary;
                    
                    saveData();
                    applySettings();
                    closeModal(elements.colorBgModal);
                    alert('背景应用成功！');
                }
            }
        }

        // 应用字体与标题
        function applyFontsAndTitle() {
            const title = document.getElementById('editTitleText').value.trim();
            const subtitle = document.getElementById('editSubtitleText').value.trim();
            const selectedTitleFont = document.querySelector('#titleFontSelector .font-option.selected');
            const selectedSubtitleFont = document.querySelector('#subtitleFontSelector .font-option.selected');
            
            if (selectedTitleFont) {
                state.settings.pageTitleFont = selectedTitleFont.dataset.font;
            }
            
            if (selectedSubtitleFont) {
                state.settings.pageSubtitleFont = selectedSubtitleFont.dataset.font;
            }
            
            state.settings.pageTitle = title;
            state.settings.pageSubtitle = subtitle;
            state.settings.pageTitleFontSize = document.getElementById('titleFontSize').value + 'px';
            
            // 处理标题图标
            if (state.titleIconPreview) {
                state.settings.pageTitleIcon = state.titleIconPreview;
            }
            
            saveData();
            applySettings();
            closeModal(elements.colorBgModal);
            
            alert('字体与标题应用成功！');
        }

        // 应用行数更改
        function applyRowsChange() {
            const action = state.rowsChangeAction;
            const target = state.rowsApplyTarget;
            
            if (action === 'add') {
                if (target === 'current' || target === 'all') {
                    const currentRows = state.settings.rowsPerCategory;
                    if (currentRows >= 8) {
                        alert('最多只能有8行');
                        return;
                    }
                    state.settings.rowsPerCategory = currentRows + 1;
                    saveData();
                }
                
                if (target === 'all') {
                    const hiddenRows = state.hiddenData.settings.rowsPerCategory;
                    if (hiddenRows >= 8) {
                        alert('最多只能有8行');
                        return;
                    }
                    state.hiddenData.settings.rowsPerCategory = hiddenRows + 1;
                    saveHiddenData();
                }
            } else if (action === 'remove') {
                if (target === 'current' || target === 'all') {
                    const currentRows = state.settings.rowsPerCategory;
                    if (currentRows <= 1) {
                        alert('至少需要1行');
                        return;
                    }
                    state.settings.rowsPerCategory = currentRows - 1;
                    saveData();
                }
                
                if (target === 'all') {
                    const hiddenRows = state.hiddenData.settings.rowsPerCategory;
                    if (hiddenRows <= 1) {
                        alert('至少需要1行');
                        return;
                    }
                    state.hiddenData.settings.rowsPerCategory = hiddenRows - 1;
                    saveHiddenData();
                }
            }
            
            // 重新渲染
            if (state.isHiddenPage) {
                renderHiddenBookmarks();
            } else {
                renderBookmarks();
            }
            
            if (target === 'all') {
                // 如果应用到所有页面，需要重新渲染另一个页面
                if (!state.isHiddenPage) {
                    renderHiddenBookmarks();
                }
            }
            
            state.rowsChangeAction = null;
            state.rowsApplyTarget = null;
            
            // 关闭模态框
            elements.rowsApplyModal.style.display = 'none';
            
            // 显示确认对话框
            showConfirmDialog(
                '操作成功',
                '行数更改已应用。',
                () => {
                    // 确认后关闭对话框
                    elements.confirmDialog.style.display = 'none';
                }
            );
        }

        // 切换自定义编辑模式
        function toggleEditMode() {
            state.editMode = !state.editMode;
            document.body.classList.toggle('edit-mode', state.editMode);
            
            const customizeBtn = elements.customizeBtn;
            if (state.editMode) {
                customizeBtn.innerHTML = '<i class="fas fa-check"></i> 完成编辑';
                elements.engineGrid.classList.remove('show');
                if (state.isHiddenPage) {
                    elements.hiddenEngineGrid.classList.remove('show');
                }
                elements.settingsMenu.classList.remove('show');
                setSettingsButtonMode('confirm');
            } else {
                customizeBtn.innerHTML = '<i class="fas fa-sliders-h"></i> 自定义模式';
                setSettingsButtonMode('settings');
            }
            
            updateSearchFunctionState();
            
            if (state.isHiddenPage) {
                renderHiddenCategories();
                renderHiddenBookmarks();
            } else {
                renderCategories();
                renderBookmarks();
            }
        }

        // 设置按钮模式
        function setSettingsButtonMode(mode) {
            state.settingsBtnMode = mode;
            const settingsBtn = elements.settingsBtn;
            
            if (mode === 'confirm') {
                settingsBtn.innerHTML = '<i class="fas fa-check"></i>';
                settingsBtn.classList.add('confirm-mode');
            } else {
                settingsBtn.innerHTML = '<i class="fas fa-cog"></i>';
                settingsBtn.classList.remove('confirm-mode');
            }
        }

        // 设置按钮点击事件
        function handleSettingsButtonClick() {
            if (state.settingsBtnMode === 'confirm') {
                if (state.editMode) {
                    toggleEditMode();
                }
            } else {
                toggleSettingsMenu();
            }
        }

        // 执行搜索
        function performSearch(isHidden = false) {
            if (state.editMode) return;
            
            const searchInput = isHidden ? elements.hiddenSearchInput : elements.searchInput;
            const query = searchInput.value.trim();
            if (!query) return;
            
            const engineKey = isHidden ? 
                state.hiddenData.settings.searchEngine : 
                state.settings.searchEngine;
            const engine = state.searchEngines[engineKey];
            const searchUrl = engine.url + encodeURIComponent(query);
            
            window.open(searchUrl, '_blank');
            searchInput.value = '';
        }

        // 处理直接输入网址
        function handleDirectUrl(input, isHidden = false) {
            if (state.editMode) return false;
            
            let url = input.trim();
            const urlPattern = /^(https?:\/\/)?([\w-]+\.)+[\w-]+(\/[\w- .\/?%&=]*)?$/i;
            
            if (urlPattern.test(url)) {
                if (!url.startsWith('http://') && !url.startsWith('https://')) {
                    url = 'https://' + url;
                }
                window.open(url, '_blank');
                return true;
            }
            
            return false;
        }

        // 关闭模态框
        function closeModal(modal) {
            modal.style.display = 'none';
            
            // 如果当前是编辑模式，则保持对钩，否则恢复齿轮
            if (state.editMode) {
                setSettingsButtonMode('confirm');
            } else {
                setSettingsButtonMode('settings');
            }
            
            state.currentAction = null;
            
            // 清除表单数据
            if (modal === elements.editBookmarkModal) {
                document.getElementById('editBookmarkForm').removeAttribute('data-hidden');
            }
            if (modal === elements.addCategoryModal) {
                document.getElementById('addCategoryForm').removeAttribute('data-hidden');
            }
            if (modal === elements.editCategoryModal) {
                document.getElementById('editCategoryForm').removeAttribute('data-hidden');
            }
        }

        // 恢复默认设置
        function resetToDefault() {
            if (confirm('确定要恢复默认设置吗？这将重置所有网站、分类和设置。')) {
                localStorage.removeItem('navPageData');
                localStorage.removeItem('navPageHiddenData');
                location.reload();
            }
            elements.settingsMenu.classList.remove('show');
        }

        // 切换设置菜单显示
        function toggleSettingsMenu() {
            elements.settingsMenu.classList.toggle('show');
        }

        // 打开导入导出模态框
        function openImportExportModal() {
            elements.importDataText.value = '';
            elements.importFileInput.value = '';
            elements.importError.classList.remove('show');
            elements.importExportModal.style.display = 'flex';
            elements.settingsMenu.classList.remove('show');
        }

        // 导出数据
        function exportData() {
            const dataToExport = {
                main: {
                    categories: state.categories,
                    bookmarks: state.bookmarks,
                    settings: state.settings
                },
                hidden: {
                    categories: state.hiddenData.categories,
                    bookmarks: state.hiddenData.bookmarks,
                    settings: state.hiddenData.settings
                },
                exportDate: new Date().toISOString(),
                version: '2.0'
            };
            
            const dataStr = JSON.stringify(dataToExport, null, 2);
            const dataBlob = new Blob([dataStr], { type: 'text/plain' });
            const url = URL.createObjectURL(dataBlob);
            
            const a = document.createElement('a');
            a.href = url;
            a.download = `导航页备份_${new Date().toISOString().split('T')[0]}.txt`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            alert('数据导出成功！');
        }

        // 导入数据 - 自动备份后导入
        function importData() {
            const dataText = elements.importDataText.value.trim();
            if (!dataText) {
                elements.importError.textContent = '请输入要导入的数据';
                elements.importError.classList.add('show');
                return;
            }
            
            try {
                const importedData = JSON.parse(dataText);
                
                // 验证数据格式
                if (!importedData.main || !importedData.hidden) {
                    throw new Error('数据格式不正确');
                }
                
                // 自动备份当前数据
                const backupData = {
                    main: {
                        categories: state.categories,
                        bookmarks: state.bookmarks,
                        settings: state.settings
                    },
                    hidden: {
                        categories: state.hiddenData.categories,
                        bookmarks: state.hiddenData.bookmarks,
                        settings: state.hiddenData.settings
                    },
                    backupDate: new Date().toISOString()
                };
                
                const backupStr = JSON.stringify(backupData, null, 2);
                const backupBlob = new Blob([backupStr], { type: 'text/plain' });
                const backupUrl = URL.createObjectURL(backupBlob);
                
                const a = document.createElement('a');
                a.href = backupUrl;
                a.download = `自动备份_${new Date().toISOString().split('T')[0]}_${new Date().getTime()}.txt`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(backupUrl);
                
                // 确认是否覆盖
                if (!confirm('已自动备份当前数据，是否继续导入新数据？')) {
                    return;
                }
                
                // 导入数据
                state.categories = importedData.main.categories;
                state.bookmarks = importedData.main.bookmarks;
                state.settings = importedData.main.settings;
                
                state.hiddenData.categories = importedData.hidden.categories;
                state.hiddenData.bookmarks = importedData.hidden.bookmarks;
                state.hiddenData.settings = importedData.hidden.settings;
                
                // 确保设置存在
                ensureSettings();
                ensureHiddenSettings();
                
                // 确保order字段
                ensureOrderFields();
                ensureHiddenOrderFields();
                
                // 清除旧的favicon缓存
                state.faviconCache = {};
                
                // 确保书签有customIcon字段
                state.bookmarks.forEach(bookmark => {
                    if (!bookmark.customIcon) {
                        bookmark.customIcon = null;
                    }
                });
                
                state.hiddenData.bookmarks.forEach(bookmark => {
                    if (!bookmark.customIcon) {
                        bookmark.customIcon = null;
                    }
                });
                
                // 保存到本地存储
                saveData();
                saveHiddenData();
                
                // 重新渲染页面
                renderCategories();
                renderBookmarks();
                applySettings();
                
                renderHiddenCategories();
                renderHiddenBookmarks();
                applyHiddenSettings();
                
                // 设置当前分类
                if (state.categories.length > 0) {
                    state.currentCategory = state.categories[0].id;
                    setActiveCategory(state.currentCategory, true);
                }
                
                if (state.hiddenData.categories.length > 0) {
                    state.hiddenData.currentCategory = state.hiddenData.categories[0].id;
                    setHiddenActiveCategory(state.hiddenData.currentCategory, true);
                }
                
                // 关闭模态框
                closeModal(elements.importExportModal);
                elements.importError.classList.remove('show');
                
                alert('数据导入成功！已自动备份当前数据。');
            } catch (error) {
                console.error('导入错误:', error);
                elements.importError.textContent = '数据格式错误，请检查导入的内容';
                elements.importError.classList.add('show');
            }
        }

        // 切换页面
        function switchPage(toHidden) {
            state.isHiddenPage = toHidden;
            
            if (toHidden) {
                elements.mainContainer.style.display = 'none';
                elements.hiddenContainer.style.display = 'block';
                elements.pageSwitcherRight.style.display = 'none';
                elements.pageSwitcherLeft.style.display = 'flex';
            } else {
                elements.mainContainer.style.display = 'block';
                elements.hiddenContainer.style.display = 'none';
                elements.pageSwitcherRight.style.display = 'flex';
                elements.pageSwitcherLeft.style.display = 'none';
            }
            
            // 更新编辑模式状态
            if (state.editMode) {
                toggleEditMode();
            }
        }

        // 显示确认对话框
        function showConfirmDialog(title, message, onConfirm) {
            elements.confirmDialogTitle.textContent = title;
            elements.confirmDialogMessage.textContent = message;
            elements.confirmDialog.style.display = 'flex';
            
            // 设置确认按钮事件
            elements.confirmDialogConfirmBtn.onclick = () => {
                if (onConfirm) onConfirm();
                elements.confirmDialog.style.display = 'none';
            };
            
            // 设置取消按钮事件
            elements.confirmDialogCancelBtn.onclick = () => {
                elements.confirmDialog.style.display = 'none';
            };
        }

        // 设置事件监听器
        function setupEventListeners() {
            // 设置按钮
            elements.settingsBtn.addEventListener('click', handleSettingsButtonClick);
            
            // 设置菜单项
            elements.customizeBtn.addEventListener('click', () => {
                toggleEditMode();
                elements.settingsMenu.classList.remove('show');
            });
            
            elements.colorBgBtn.addEventListener('click', openColorBgModal);
            elements.importExportBtn.addEventListener('click', openImportExportModal);
            elements.resetBtn.addEventListener('click', resetToDefault);
            
            // 搜索引擎选择
            elements.currentEngine.addEventListener('click', () => {
                if (state.editMode) return;
                elements.engineGrid.classList.toggle('show');
            });
            
            elements.hiddenCurrentEngine.addEventListener('click', () => {
                if (state.editMode) return;
                elements.hiddenEngineGrid.classList.toggle('show');
            });
            
            // 搜索按钮
            elements.searchBtn.addEventListener('click', () => performSearch(false));
            elements.hiddenSearchBtn.addEventListener('click', () => performSearch(true));
            
            // 搜索框回车事件
            elements.searchInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    const query = elements.searchInput.value.trim();
                    if (!handleDirectUrl(query, false)) {
                        performSearch(false);
                    }
                }
            });
            
            elements.hiddenSearchInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    const query = elements.hiddenSearchInput.value.trim();
                    if (!handleDirectUrl(query, true)) {
                        performSearch(true);
                    }
                }
            });
            
            // 编辑网站表单
            document.getElementById('editBookmarkForm').addEventListener('submit', saveBookmark);
            document.getElementById('closeEditModalBtn').addEventListener('click', () => closeModal(elements.editBookmarkModal));
            document.getElementById('cancelEditBtn').addEventListener('click', () => closeModal(elements.editBookmarkModal));
            
            // 添加分类表单
            document.getElementById('addCategoryForm').addEventListener('submit', saveAddCategory);
            document.getElementById('closeAddCategoryModalBtn').addEventListener('click', () => closeModal(elements.addCategoryModal));
            document.getElementById('cancelAddCategoryBtn').addEventListener('click', () => closeModal(elements.addCategoryModal));
            
            // 编辑分类表单
            document.getElementById('editCategoryForm').addEventListener('submit', saveCategory);
            document.getElementById('closeCategoryModalBtn').addEventListener('click', () => closeModal(elements.editCategoryModal));
            document.getElementById('cancelCategoryEditBtn').addEventListener('click', () => closeModal(elements.editCategoryModal));
            
            // 配色和背景模态框
            document.getElementById('closeColorBgModalBtn').addEventListener('click', () => closeModal(elements.colorBgModal));
            
            // 标签页切换
            document.querySelectorAll('.color-tab').forEach(tab => {
                tab.addEventListener('click', () => {
                    const tabId = tab.dataset.tab;
                    
                    document.querySelectorAll('.color-tab').forEach(t => {
                        t.classList.remove('active');
                    });
                    tab.classList.add('active');
                    
                    document.querySelectorAll('.color-tab-content').forEach(content => {
                        content.classList.remove('active');
                    });
                    document.getElementById(`${tabId}Tab`).classList.add('active');
                });
            });
            
            // 皮肤应用按钮
            document.getElementById('applySkinBtn').addEventListener('click', applySkin);
            document.getElementById('cancelSkinBtn').addEventListener('click', () => closeModal(elements.colorBgModal));
            
            // 颜色应用按钮
            document.getElementById('applyColorsBtn').addEventListener('click', applyColors);
            document.getElementById('cancelColorsBtn').addEventListener('click', () => closeModal(elements.colorBgModal));
            
            // 背景应用按钮
            document.getElementById('applyBgBtn').addEventListener('click', applyBackground);
            document.getElementById('cancelBgBtn').addEventListener('click', () => closeModal(elements.colorBgModal));
            
            // 背景选项点击事件
            document.querySelectorAll('.bg-option').forEach(option => {
                option.addEventListener('click', () => {
                    document.querySelectorAll('.bg-option').forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    option.classList.add('selected');
                    
                    if (option.id === 'imageUpload') {
                        document.getElementById('imageUploadInput').click();
                    }
                });
            });
            
            // 文件上传事件
            document.getElementById('imageUploadInput').addEventListener('change', function() {
                const selectedOption = document.getElementById('imageUpload');
                document.querySelectorAll('.bg-option').forEach(opt => {
                    opt.classList.remove('selected');
                });
                selectedOption.classList.add('selected');
            });
            
            // 字体与标题应用按钮
            document.getElementById('applyFontsBtn').addEventListener('click', applyFontsAndTitle);
            document.getElementById('cancelFontsBtn').addEventListener('click', () => closeModal(elements.colorBgModal));
            
            // 标题图标上传
            document.getElementById('titleIconUpload').addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (file) {
                    if (!file.type.startsWith('image/')) {
                        alert('请选择图片文件');
                        return;
                    }
                    
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        document.getElementById('titleIconPreview').src = e.target.result;
                        document.getElementById('titleIconPreview').style.display = 'block';
                        state.titleIconPreview = e.target.result;
                    };
                    reader.readAsDataURL(file);
                }
            });
            
            // 移除标题图标
            document.getElementById('removeTitleIconBtn').addEventListener('click', function() {
                document.getElementById('titleIconPreview').src = '';
                document.getElementById('titleIconPreview').style.display = 'none';
                state.titleIconPreview = null;
            });
            
            // 字体大小滑块
            document.getElementById('titleFontSize').addEventListener('input', function() {
                document.getElementById('fontSizeValue').textContent = this.value + 'px';
            });
            
            // 导入导出相关
            document.getElementById('closeImportExportModalBtn').addEventListener('click', () => closeModal(elements.importExportModal));
            document.getElementById('cancelImportExportBtn').addEventListener('click', () => closeModal(elements.importExportModal));
            document.getElementById('exportDataBtn').addEventListener('click', exportData);
            document.getElementById('importDataBtn').addEventListener('click', importData);
            
            // 文件导入
            document.getElementById('importFileInput').addEventListener('change', function(e) {
                const file = e.target.files[0];
                if (file) {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        elements.importDataText.value = e.target.result;
                    };
                    reader.readAsDataURL(file);
                }
            });
            
            // 确认对话框
            document.getElementById('confirmDialogCancelBtn').addEventListener('click', () => {
                elements.confirmDialog.style.display = 'none';
            });
            
            // 行数应用选择
            document.getElementById('closeRowsApplyModalBtn').addEventListener('click', () => {
                elements.rowsApplyModal.style.display = 'none';
            });
            
            document.getElementById('applyToCurrentPageBtn').addEventListener('click', () => {
                state.rowsApplyTarget = 'current';
                applyRowsChange();
            });
            
            document.getElementById('applyToAllPagesBtn').addEventListener('click', () => {
                state.rowsApplyTarget = 'all';
                applyRowsChange();
            });
            
            document.getElementById('cancelRowsApplyBtn').addEventListener('click', () => {
                elements.rowsApplyModal.style.display = 'none';
            });
            
            // 页面切换
            elements.pageSwitcherRight.addEventListener('click', () => switchPage(true));
            elements.pageSwitcherLeft.addEventListener('click', () => switchPage(false));
            
            // 点击页面其他地方关闭搜索引擎网格
            document.addEventListener('click', (e) => {
                if (!e.target.closest('.search-engine-selector')) {
                    elements.engineGrid.classList.remove('show');
                    elements.hiddenEngineGrid.classList.remove('show');
                }
                
                // 点击其他地方关闭设置菜单
                if (!e.target.closest('.settings-btn') && !e.target.closest('.settings-menu')) {
                    elements.settingsMenu.classList.remove('show');
                }
            });
            
            // 点击模态框外部关闭模态框
            document.querySelectorAll('.modal').forEach(modal => {
                modal.addEventListener('click', (e) => {
                    if (e.target === modal) {
                        closeModal(modal);
                    }
                });
            });
        }

        // 页面加载完成后初始化应用
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
