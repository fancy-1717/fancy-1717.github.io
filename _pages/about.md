---
permalink: /
title: "Academic Pages is a ready-to-fork GitHub Pages template for academic personal websites"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>看房信息记录系统</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
    <!-- 引入SheetJS库用于导出Excel -->
    <script src="https://cdn.sheetjs.com/xlsx-0.19.3/package/dist/xlsx.full.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: white;
            min-height: 100vh;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        /* 头部样式 */
        .header {
            background: linear-gradient(135deg, #1e88e5, #0d47a1);
            color: white;
            padding: 20px 15px;
            text-align: center;
            position: relative;
            z-index: 10;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        
        .header h1 {
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 5px;
        }
        
        .header p {
            font-size: 0.85rem;
            opacity: 0.9;
        }
        
        .back-button {
            background: none;
            border: none;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            padding: 5px;
            margin-right: 10px;
        }
        
        .header-title {
            flex: 1;
            text-align: center;
        }
        
        /* 底部导航 */
        .tab-bar {
            display: flex;
            position: fixed;
            bottom: 0;
            width: 100%;
            max-width: 500px;
            background: white;
            border-top: 1px solid #eee;
            z-index: 100;
        }
        
        .tab-item {
            flex: 1;
            text-align: center;
            padding: 12px 0;
            color: #999;
            font-size: 0.75rem;
            transition: all 0.3s ease;
        }
        
        .tab-item.active {
            color: #1e88e5;
        }
        
        .tab-item i {
            display: block;
            font-size: 1.2rem;
            margin-bottom: 4px;
        }
        
        /* 首页内容 */
        .home-content {
            padding: 20px;
            padding-bottom: 70px; /* 避免内容被底部导航遮挡 */
        }
        
        .section-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 15px;
            color: #1e88e5;
            padding-bottom: 8px;
            border-bottom: 2px solid #e3f2fd;
        }
        
        .card-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 30px;
        }
        
        .card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            cursor: pointer;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 16px rgba(0, 0, 0, 0.12);
        }
        
        .card-header {
            background: #1e88e5;
            color: white;
            padding: 15px;
            text-align: center;
        }
        
        .card-header i {
            font-size: 2rem;
            margin-bottom: 10px;
        }
        
        .card-body {
            padding: 15px;
            text-align: center;
            background: #f9f9f9;
        }
        
        .card-body h3 {
            margin-bottom: 8px;
            color: #333;
        }
        
        .card-body p {
            font-size: 0.85rem;
            color: #666;
        }
        
        .recent-records {
            background: white;
            border-radius: 12px;
            padding: 15px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            max-height: 300px;
            overflow-y: auto;
        }
        
        .record-list {
            list-style: none;
        }
        
        .record-item {
            padding: 12px 0;
            border-bottom: 1px solid #eee;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.2s;
            position: relative;
        }
        
        .record-item:hover {
            background-color: #f5f7fa;
        }
        
        .record-item:last-child {
            border-bottom: none;
        }
        
        .record-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: #e3f2fd;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 12px;
            color: #1e88e5;
        }
        
        .record-info {
            flex: 1;
        }
        
        .record-info h4 {
            font-size: 0.95rem;
            margin-bottom: 4px;
        }
        
        .record-info p {
            font-size: 0.8rem;
            color: #888;
        }
        
        .delete-btn {
            background: none;
            border: none;
            color: #ff6b6b;
            font-size: 1rem;
            cursor: pointer;
            padding: 5px 10px;
            opacity: 0.7;
            transition: opacity 0.3s;
        }
        
        .delete-btn:hover {
            opacity: 1;
        }
        
        /* 表单页面样式 */
        .form-container {
            padding: 20px;
            padding-bottom: 70px;
            max-height: calc(100vh - 100px);
            overflow-y: auto;
        }
        
        .form-section {
            margin-bottom: 25px;
            background: white;
            border-radius: 12px;
            padding: 15px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .form-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #e3f2fd;
            color: #1e88e5;
        }
        
        .form-group {
            display: flex;
            margin-bottom: 15px;
            align-items: center;
        }
        
        .form-label {
            width: 100px;
            font-size: 0.9rem;
            color: #555;
        }
        
        .form-input {
            flex: 1;
            padding: 10px 12px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 0.9rem;
            transition: border 0.3s ease;
        }
        
        .form-input:focus {
            outline: none;
            border-color: #1e88e5;
            box-shadow: 0 0 0 2px rgba(30, 136, 229, 0.2);
        }
        
        select.form-input {
            appearance: none;
            background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='%23333' viewBox='0 0 16 16'%3E%3Cpath d='M8 11L3 6h10z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 12px center;
            padding-right: 35px;
        }
        
        textarea.form-input {
            min-height: 80px;
            resize: vertical;
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }
        
        .btn-primary {
            background: #1e88e5;
            color: white;
        }
        
        .btn-primary:hover {
            background: #1565c0;
        }
        
        .btn-outline {
            background: white;
            border: 1px solid #1e88e5;
            color: #1e88e5;
        }
        
        .btn-outline:hover {
            background: #e3f2fd;
        }
        
        .btn-danger {
            background: #ff6b6b;
            color: white;
        }
        
        .btn-danger:hover {
            background: #ff5252;
        }
        
        /* 页面切换动画 */
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* 详情页面样式 */
        .detail-container {
            padding: 20px;
            padding-bottom: 70px;
        }
        
        .detail-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .detail-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .detail-title {
            font-size: 1.3rem;
            font-weight: 600;
            color: #1e88e5;
        }
        
        .detail-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: #e3f2fd;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #1e88e5;
            font-size: 1.5rem;
        }
        
        .detail-info {
            margin-bottom: 20px;
        }
        
        .detail-item {
            display: flex;
            margin-bottom: 12px;
            padding-bottom: 12px;
            border-bottom: 1px dashed #eee;
        }
        
        .detail-label {
            width: 100px;
            font-weight: 500;
            color: #666;
        }
        
        .detail-value {
            flex: 1;
            color: #333;
        }
        
        .detail-section {
            margin-bottom: 25px;
        }
        
        .detail-section-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 15px;
            color: #1e88e5;
            padding-bottom: 8px;
            border-bottom: 2px solid #e3f2fd;
        }
        
        /* 照片上传区域 */
        .photo-upload {
            margin-top: 20px;
        }
        
        .photo-upload-label {
            display: block;
            margin-bottom: 10px;
            font-weight: 500;
            color: #555;
        }
        
        .photo-preview-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }
        
        .photo-preview {
            width: 80px;
            height: 80px;
            border-radius: 8px;
            overflow: hidden;
            position: relative;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
            cursor: pointer;
        }
        
        .photo-preview img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .photo-preview .delete-photo {
            position: absolute;
            top: 2px;
            right: 2px;
            background: rgba(0, 0, 0, 0.5);
            color: white;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            cursor: pointer;
        }
        
        .add-photo-btn {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 80px;
            height: 80px;
            border: 2px dashed #ccc;
            border-radius: 8px;
            color: #888;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .add-photo-btn:hover {
            border-color: #1e88e5;
            color: #1e88e5;
        }
        
        .add-photo-btn i {
            font-size: 1.5rem;
            margin-bottom: 5px;
        }
        
        .file-input {
            display: none;
        }
        
        /* 照片查看模态框 */
        .photo-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s;
        }
        
        .photo-modal.active {
            opacity: 1;
            pointer-events: all;
        }
        
        .modal-content {
            position: relative;
            max-width: 90%;
            max-height: 90%;
        }
        
        .modal-content img {
            max-width: 100%;
            max-height: 80vh;
            border-radius: 8px;
        }
        
        .modal-close {
            position: absolute;
            top: 15px;
            right: 15px;
            color: white;
            background: rgba(0, 0, 0, 0.5);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 10;
        }
        
        .modal-nav {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            color: white;
            background: rgba(0, 0, 0, 0.5);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 10;
        }
        
        .prev-btn {
            left: 15px;
        }
        
        .next-btn {
            right: 15px;
        }
        
        /* 响应式调整 */
        @media (max-width: 480px) {
            .card-container {
                grid-template-columns: 1fr;
            }
            
            .form-label {
                width: 90px;
            }
        }
        
        /* 提示信息 */
        .toast {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 10px 20px;
            border-radius: 20px;
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .toast.show {
            opacity: 1;
        }
        
        /* 我的页面样式 */
        .user-content {
            padding: 20px;
            padding-bottom: 70px;
        }
        
        .user-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            text-align: center;
        }
        
        .avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: #e3f2fd;
            margin: 0 auto 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: #1e88e5;
        }
        
        .stat-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }
        
        .stat-card {
            background: #f9f9f9;
            border-radius: 10px;
            padding: 15px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: #1e88e5;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.85rem;
            color: #666;
        }
        
        /* 管理页面样式 */
        .manage-section {
            background: white;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .record-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }
        
        .record-table th, .record-table td {
            padding: 12px 10px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        
        .record-table th {
            background-color: #f5f7fa;
            font-weight: 600;
            color: #555;
        }
        
        .record-table tr:last-child td {
            border-bottom: none;
        }
        
        .record-table tr:hover {
            background-color: #f9f9f9;
        }
        
        .action-btn {
            background: none;
            border: none;
            color: #1e88e5;
            cursor: pointer;
            margin-left: 8px;
            font-size: 0.9rem;
        }
        
        .delete-action {
            color: #ff6b6b;
        }
        
        /* 空状态样式 */
        .empty-state {
            text-align: center;
            padding: 30px 0;
            color: #888;
        }
        
        .empty-state i {
            font-size: 3rem;
            margin-bottom: 15px;
            color: #ddd;
        }
        
        /* 确认删除模态框 */
        .delete-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1001;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s;
        }
        
        .delete-modal.active {
            opacity: 1;
            pointer-events: all;
        }
        
        .modal-content-card {
            background: white;
            border-radius: 12px;
            padding: 25px;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            text-align: center;
        }
        
        .modal-title {
            font-size: 1.2rem;
            font-weight: 600;
            margin-bottom: 15px;
            color: #333;
        }
        
        .modal-message {
            margin-bottom: 25px;
            color: #555;
            line-height: 1.5;
        }
        
        .modal-buttons {
            display: flex;
            gap: 15px;
        }
        
        .modal-btn {
            flex: 1;
            padding: 10px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 500;
            cursor: pointer;
        }
        
        .modal-cancel {
            background: #f0f0f0;
            color: #555;
        }
        
        .modal-confirm {
            background: #ff6b6b;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 头部 -->
        <div class="header">
            <button class="back-button" id="back-button" style="display: none;">
                <i class="fas fa-arrow-left"></i>
            </button>
            <div class="header-title">
                <h1>看房信息记录系统</h1>
                <p>便捷记录楼盘与房源信息</p>
            </div>
            <div style="width: 48px;"></div> <!-- 占位元素保持标题居中 -->
        </div>
        
        <!-- 首页 -->
        <div id="home-page" class="page active">
            <div class="home-content">
                <h2 class="section-title">功能模块</h2>
                <div class="card-container">
                    <div class="card" onclick="showPage('project-page')">
                        <div class="card-header">
                            <i class="fas fa-building"></i>
                            <h3>记录楼盘</h3>
                        </div>
                        <div class="card-body">
                            <p>添加新楼盘信息及周边配套</p>
                        </div>
                    </div>
                    
                    <div class="card" onclick="showPage('house-page')">
                        <div class="card-header">
                            <i class="fas fa-home"></i>
                            <h3>记录房源</h3>
                        </div>
                        <div class="card-body">
                            <p>添加房源信息及交易详情</p>
                        </div>
                    </div>
                </div>
                
                <h2 class="section-title">最近记录</h2>
                <div class="recent-records">
                    <ul class="record-list" id="recent-records-list">
                        <!-- 动态生成最近记录 -->
                    </ul>
                </div>
            </div>
        </div>
        
        <!-- 记录楼盘页面 -->
        <div id="project-page" class="page">
            <div class="form-container">
                <div class="form-section">
                    <h3 class="form-title">周边配套</h3>
                    <div class="form-group">
                        <label class="form-label">楼盘名称</label>
                        <input type="text" class="form-input" id="project-name" placeholder="请输入楼盘名称">
                    </div>
                    <div class="form-group">
                        <label class="form-label">交通</label>
                        <input type="text" class="form-input" id="project-traffic" placeholder="地铁/公交线路">
                    </div>
                    <div class="form-group">
                        <label class="form-label">超市</label>
                        <input type="text" class="form-input" id="project-market" placeholder="附近超市">
                    </div>
                    <div class="form-group">
                        <label class="form-label">商业</label>
                        <input type="text" class="form-input" id="project-business" placeholder="商业配套">
                    </div>
                    <div class="form-group">
                        <label class="form-label">医疗</label>
                        <input type="text" class="form-input" id="project-medical" placeholder="医院/诊所">
                    </div>
                    <div class="form-group">
                        <label class="form-label">小学</label>
                        <input type="text" class="form-input" id="project-primary" placeholder="附近小学">
                    </div>
                    <div class="form-group">
                        <label class="form-label">中学</label>
                        <input type="text" class="form-input" id="project-middle" placeholder="附近中学">
                    </div>
                    <div class="form-group">
                        <label class="form-label">备注</label>
                        <textarea class="form-input" id="project-periphery-remark" placeholder="其他配套信息"></textarea>
                    </div>
                </div>
                
                <div class="form-section">
                    <h3 class="form-title">楼盘信息</h3>
                    <div class="form-group">
                        <label class="form-label">建成时间</label>
                        <input type="text" class="form-input" id="project-built-year" placeholder="如：2020年">
                    </div>
                    <div class="form-group">
                        <label class="form-label">绿化率</label>
                        <input type="text" class="form-input" id="project-greening" placeholder="如：35%">
                    </div>
                    <div class="form-group">
                        <label class="form-label">容积率</label>
                        <input type="text" class="form-input" id="project-plot-ratio" placeholder="如：2.5">
                    </div>
                    <div class="form-group">
                        <label class="form-label">物业</label>
                        <input type="text" class="form-input" id="project-property" placeholder="物业公司">
                    </div>
                    <div class="form-group">
                        <label class="form-label">车位</label>
                        <input type="text" class="form-input" id="project-parking" placeholder="车位情况">
                    </div>
                    <div class="form-group">
                        <label class="form-label">备注</label>
                        <textarea class="form-input" id="project-info-remark" placeholder="其他楼盘信息"></textarea>
                    </div>
                </div>
                
                <!-- 照片上传区域 -->
                <div class="form-section">
                    <h3 class="form-title">楼盘照片</h3>
                    <div class="photo-upload">
                        <div class="photo-preview-container" id="project-photos-preview">
                            <div class="add-photo-btn" onclick="document.getElementById('project-photo-input').click()">
                                <i class="fas fa-plus"></i>
                                <span>添加照片</span>
                            </div>
                        </div>
                        <input type="file" id="project-photo-input" class="file-input" accept="image/*" multiple>
                    </div>
                </div>
                
                <div class="button-group">
                    <button class="btn btn-outline" onclick="showPage('home-page')">取消</button>
                    <button class="btn btn-primary" onclick="saveProject()">保存楼盘</button>
                </div>
            </div>
        </div>
        
        <!-- 记录房源页面 -->
        <div id="house-page" class="page">
            <div class="form-container">
                <div class="form-section">
                    <h3 class="form-title">房源信息</h3>
                    <div class="form-group">
                        <label class="form-label">所属楼盘</label>
                        <select class="form-input" id="house-project">
                            <option value="">请选择楼盘</option>
                            <!-- 楼盘选项将通过JS动态添加 -->
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">总价(万元)</label>
                        <input type="number" class="form-input" id="house-total-price" placeholder="请输入总价">
                    </div>
                    <div class="form-group">
                        <label class="form-label">面积(㎡)</label>
                        <input type="number" class="form-input" id="house-area" placeholder="建筑面积">
                    </div>
                    <div class="form-group">
                        <label class="form-label">单价(元/㎡)</label>
                        <input type="text" class="form-input" id="house-unit-price" placeholder="自动计算" readonly>
                    </div>
                    <div class="form-group">
                        <label class="form-label">电梯</label>
                        <select class="form-input" id="house-elevator">
                            <option value="">请选择</option>
                            <option value="有电梯">有电梯</option>
                            <option value="无电梯">无电梯</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">楼层</label>
                        <input type="text" class="form-input" id="house-floor" placeholder="如：12/28">
                    </div>
                    <div class="form-group">
                        <label class="form-label">房号</label>
                        <input type="text" class="form-input" id="house-number" placeholder="如：3栋1202">
                    </div>
                    <div class="form-group">
                        <label class="form-label">户型</label>
                        <input type="text" class="form-input" id="house-layout" placeholder="如：三室两厅一卫">
                    </div>
                    <div class="form-group">
                        <label class="form-label">车位</label>
                        <input type="text" class="form-input" id="house-parking" placeholder="车位情况">
                    </div>
                    <div class="form-group">
                        <label class="form-label">朝向</label>
                        <input type="text" class="form-input" id="house-orientation" placeholder="如：南向">
                    </div>
                    <div class="form-group">
                        <label class="form-label">装修</label>
                        <select class="form-input" id="house-decoration">
                            <option value="">请选择</option>
                            <option value="毛坯">毛坯</option>
                            <option value="简装">简装</option>
                            <option value="精装">精装</option>
                            <option value="豪装">豪装</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label class="form-label">备注</label>
                        <textarea class="form-input" id="house-info-remark" placeholder="其他房源信息"></textarea>
                    </div>
                </div>
                
                <div class="form-section">
                    <h3 class="form-title">交易信息</h3>
                    <div class="form-group">
                        <label class="form-label">契税</label>
                        <input type="text" class="form-input" id="house-deed-tax" placeholder="契税金额">
                    </div>
                    <div class="form-group">
                        <label class="form-label">房产税</label>
                        <input type="text" class="form-input" id="house-property-tax" placeholder="房产税金额">
                    </div>
                    <div class="form-group">
                        <label class="form-label">增值税</label>
                        <input type="text" class="form-input" id="house-vat" placeholder="增值税金额">
                    </div>
                    <div class="form-group">
                        <label class="form-label">备注</label>
                        <textarea class="form-input" id="house-transaction-remark" placeholder="其他交易信息"></textarea>
                    </div>
                </div>
                
                <!-- 照片上传区域 -->
                <div class="form-section">
                    <h3 class="form-title">房源照片</h3>
                    <div class="photo-upload">
                        <div class="photo-preview-container" id="house-photos-preview">
                            <div class="add-photo-btn" onclick="document.getElementById('house-photo-input').click()">
                                <i class="fas fa-plus"></i>
                                <span>添加照片</span>
                            </div>
                        </div>
                        <input type="file" id="house-photo-input" class="file-input" accept="image/*" multiple>
                    </div>
                </div>
                
                <div class="button-group">
                    <button class="btn btn-outline" onclick="showPage('home-page')">取消</button>
                    <button class="btn btn-primary" onclick="saveHouse()">保存房源</button>
                </div>
            </div>
        </div>
        
        <!-- 我的页面 -->
        <div id="my-page" class="page">
            <div class="user-content">
                <div class="user-card">
                    <div class="avatar">
                        <i class="fas fa-user"></i>
                    </div>
                    <h3>房产经纪人</h3>
                    <p>专业记录看房信息</p>
                    
                    <div class="stat-container">
                        <div class="stat-card">
                            <div class="stat-value" id="project-count">0</div>
                            <div class="stat-label">楼盘记录</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="house-count">0</div>
                            <div class="stat-label">房源记录</div>
                        </div>
                    </div>
                </div>
                
                <div class="form-section">
                    <h3 class="form-title">数据管理</h3>
                    <button class="btn btn-outline" style="width:100%; margin-bottom:15px;" onclick="exportData()">
                        <i class="fas fa-download"></i> 导出Excel数据
                    </button>
                    <button class="btn btn-outline" style="width:100%; margin-bottom:15px;" onclick="showPage('manage-projects-page')">
                        <i class="fas fa-building"></i> 管理楼盘记录
                    </button>
                    <button class="btn btn-outline" style="width:100%;" onclick="showPage('manage-houses-page')">
                        <i class="fas fa-home"></i> 管理房源记录
                    </button>
                </div>
            </div>
        </div>
        
        <!-- 楼盘详情页 -->
        <div id="project-detail-page" class="page">
            <div class="detail-container">
                <div class="detail-card">
                    <div class="detail-header">
                        <div class="detail-icon">
                            <i class="fas fa-building"></i>
                        </div>
                        <div class="detail-title" id="project-detail-name">楼盘名称</div>
                    </div>
                    
                    <div class="detail-section">
                        <h3 class="detail-section-title">基本信息</h3>
                        <div class="detail-info">
                            <div class="detail-item">
                                <div class="detail-label">建成时间</div>
                                <div class="detail-value" id="project-detail-built-year"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">绿化率</div>
                                <div class="detail-value" id="project-detail-greening"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">容积率</div>
                                <div class="detail-value" id="project-detail-plot-ratio"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">物业公司</div>
                                <div class="detail-value" id="project-detail-property"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">车位情况</div>
                                <div class="detail-value" id="project-detail-parking"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">备注</div>
                                <div class="detail-value" id="project-detail-info-remark"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="detail-section">
                        <h3 class="detail-section-title">周边配套</h3>
                        <div class="detail-info">
                            <div class="detail-item">
                                <div class="detail-label">交通</div>
                                <div class="detail-value" id="project-detail-traffic"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">超市</div>
                                <div class="detail-value" id="project-detail-market"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">商业</div>
                                <div class="detail-value" id="project-detail-business"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">医疗</div>
                                <div class="detail-value" id="project-detail-medical"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">小学</div>
                                <div class="detail-value" id="project-detail-primary"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">中学</div>
                                <div class="detail-value" id="project-detail-middle"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">备注</div>
                                <div class="detail-value" id="project-detail-periphery-remark"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="detail-section">
                        <h3 class="detail-section-title">楼盘照片</h3>
                        <div class="photo-preview-container" id="project-detail-photos">
                            <!-- 照片将通过JS动态添加 -->
                        </div>
                    </div>
                    
                    <div class="button-group">
                        <button class="btn btn-danger" onclick="confirmDelete('project', currentDetailId)">
                            <i class="fas fa-trash"></i> 删除楼盘
                        </button>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 房源详情页 -->
        <div id="house-detail-page" class="page">
            <div class="detail-container">
                <div class="detail-card">
                    <div class="detail-header">
                        <div class="detail-icon">
                            <i class="fas fa-home"></i>
                        </div>
                        <div>
                            <div class="detail-title" id="house-detail-project">楼盘名称</div>
                            <div style="font-size: 0.9rem; color: #666;" id="house-detail-number">房号</div>
                        </div>
                    </div>
                    
                    <div class="detail-section">
                        <h3 class="detail-section-title">房源信息</h3>
                        <div class="detail-info">
                            <div class="detail-item">
                                <div class="detail-label">总价</div>
                                <div class="detail-value" id="house-detail-total-price"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">面积</div>
                                <div class="detail-value" id="house-detail-area"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">单价</div>
                                <div class="detail-value" id="house-detail-unit-price"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">户型</div>
                                <div class="detail-value" id="house-detail-layout"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">楼层</div>
                                <div class="detail-value" id="house-detail-floor"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">朝向</div>
                                <div class="detail-value" id="house-detail-orientation"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">装修</div>
                                <div class="detail-value" id="house-detail-decoration"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">电梯</div>
                                <div class="detail-value" id="house-detail-elevator"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">车位</div>
                                <div class="detail-value" id="house-detail-parking"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">备注</div>
                                <div class="detail-value" id="house-detail-info-remark"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="detail-section">
                        <h3 class="detail-section-title">交易信息</h3>
                        <div class="detail-info">
                            <div class="detail-item">
                                <div class="detail-label">契税</div>
                                <div class="detail-value" id="house-detail-deed-tax"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">房产税</div>
                                <div class="detail-value" id="house-detail-property-tax"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">增值税</div>
                                <div class="detail-value" id="house-detail-vat"></div>
                            </div>
                            <div class="detail-item">
                                <div class="detail-label">备注</div>
                                <div class="detail-value" id="house-detail-transaction-remark"></div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="detail-section">
                        <h3 class="detail-section-title">房源照片</h3>
                        <div class="photo-preview-container" id="house-detail-photos">
                            <!-- 照片将通过JS动态添加 -->
                        </div>
                    </div>
                    
                    <div class="button-group">
                        <button class="btn btn-danger" onclick="confirmDelete('house', currentDetailId)">
                            <i class="fas fa-trash"></i> 删除房源
                        </button>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 管理楼盘页面 -->
        <div id="manage-projects-page" class="page">
            <div class="user-content">
                <div class="manage-section">
                    <h3 class="form-title">楼盘记录管理</h3>
                    <div id="projects-list-container">
                        <!-- 楼盘列表将通过JS动态添加 -->
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 管理房源页面 -->
        <div id="manage-houses-page" class="page">
            <div class="user-content">
                <div class="manage-section">
                    <h3 class="form-title">房源记录管理</h3>
                    <div id="houses-list-container">
                        <!-- 房源列表将通过JS动态添加 -->
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 照片查看模态框 -->
        <div class="photo-modal" id="photo-modal">
            <div class="modal-close" onclick="closePhotoModal()">
                <i class="fas fa-times"></i>
            </div>
            <div class="modal-nav prev-btn" onclick="showPrevPhoto()">
                <i class="fas fa-chevron-left"></i>
            </div>
            <div class="modal-content">
                <img id="modal-photo" src="" alt="照片">
            </div>
            <div class="modal-nav next-btn" onclick="showNextPhoto()">
                <i class="fas fa-chevron-right"></i>
            </div>
        </div>
        
        <!-- 确认删除模态框 -->
        <div class="delete-modal" id="delete-modal">
            <div class="modal-content-card">
                <h3 class="modal-title">确认删除</h3>
                <p class="modal-message" id="delete-message">您确定要删除这条记录吗？此操作不可恢复。</p>
                <div class="modal-buttons">
                    <button class="modal-btn modal-cancel" onclick="closeDeleteModal()">取消</button>
                    <button class="modal-btn modal-confirm" id="confirm-delete-btn">确认删除</button>
                </div>
            </div>
        </div>
        
        <!-- 底部导航 -->
        <div class="tab-bar">
            <div class="tab-item active" onclick="showPage('home-page')">
                <i class="fas fa-home"></i>
                <span>首页</span>
            </div>
            <div class="tab-item" onclick="showPage('my-page')">
                <i class="fas fa-user"></i>
                <span>我的</span>
            </div>
        </div>
        
        <!-- 提示信息 -->
        <div class="toast" id="toast">操作成功！</div>
    </div>

    <script>
        // 全局变量
        let currentPhotos = [];
        let currentPhotoIndex = 0;
        let currentDetailId = null;
        let currentDeleteType = null;
        let currentDeleteId = null;
        
        // 页面切换功能
        function showPage(pageId) {
            // 隐藏所有页面
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // 显示目标页面
            document.getElementById(pageId).classList.add('active');
            
            // 更新底部导航激活状态
            document.querySelectorAll('.tab-item').forEach((item, index) => {
                item.classList.remove('active');
            });
            
            // 控制返回按钮显示
            const backButton = document.getElementById('back-button');
            if(pageId === 'home-page' || pageId === 'my-page' || 
               pageId === 'manage-projects-page' || pageId === 'manage-houses-page') {
                backButton.style.display = 'none';
                document.querySelector('.header-title h1').textContent = '看房信息记录系统';
                document.querySelector('.header-title p').textContent = '便捷记录楼盘与房源信息';
            } else if(pageId === 'project-detail-page' || pageId === 'house-detail-page') {
                backButton.style.display = 'block';
            } else {
                backButton.style.display = 'block';
                document.querySelector('.header-title h1').textContent = pageId === 'project-page' ? '记录楼盘信息' : '记录房源信息';
                document.querySelector('.header-title p').textContent = '填写详细信息';
            }
            
            if(pageId === 'home-page') {
                document.querySelectorAll('.tab-item')[0].classList.add('active');
                loadRecentRecords();
            } else if(pageId === 'my-page') {
                document.querySelectorAll('.tab-item')[1].classList.add('active');
                updateStats();
            } else if(pageId === 'house-page') {
                // 当进入记录房源页面时，加载楼盘下拉菜单
                loadProjectOptions();
            } else if(pageId === 'manage-projects-page') {
                loadProjectsForManagement();
            } else if(pageId === 'manage-houses-page') {
                loadHousesForManagement();
            }
        }
        
        // 返回按钮功能
        document.getElementById('back-button').addEventListener('click', function() {
            showPage('home-page');
        });
        
        // 显示提示信息
        function showToast(message) {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 2000);
        }
        
        // 获取本地存储的数据
        function getLocalData(key) {
            const data = localStorage.getItem(key);
            return data ? JSON.parse(data) : [];
        }
        
        // 保存数据到本地存储
        function saveLocalData(key, data) {
            localStorage.setItem(key, JSON.stringify(data));
        }
        
        // 照片预览功能
        function previewPhotos(event, recordType) {
            const files = event.target.files;
            const previewContainer = document.getElementById(`${recordType}-photos-preview`);
            
            // 清空预览容器（保留添加按钮）
            previewContainer.innerHTML = '<div class="add-photo-btn" onclick="document.getElementById(\'' + recordType + '-photo-input\').click()"><i class="fas fa-plus"></i><span>添加照片</span></div>';
            
            // 预览新选择的照片
            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    const photoPreview = document.createElement('div');
                    photoPreview.className = 'photo-preview';
                    photoPreview.innerHTML = `
                        <img src="${e.target.result}" alt="照片预览">
                        <div class="delete-photo" onclick="deletePreviewPhoto(this)">×</div>
                    `;
                    
                    // 在添加按钮前插入新照片
                    previewContainer.insertBefore(photoPreview, previewContainer.firstChild);
                };
                
                reader.readAsDataURL(file);
            }
        }
        
        // 删除预览照片
        function deletePreviewPhoto(element) {
            element.parentElement.remove();
        }
        
        // 打开照片查看模态框
        function openPhotoModal(photos, index, recordId, recordType) {
            currentPhotos = photos;
            currentPhotoIndex = index;
            
            document.getElementById('modal-photo').src = photos[index];
            document.getElementById('photo-modal').classList.add('active');
        }
        
        // 关闭照片查看模态框
        function closePhotoModal() {
            document.getElementById('photo-modal').classList.remove('active');
        }
        
        // 显示下一张照片
        function showNextPhoto() {
            if (currentPhotoIndex < currentPhotos.length - 1) {
                currentPhotoIndex++;
                document.getElementById('modal-photo').src = currentPhotos[currentPhotoIndex];
            }
        }
        
        // 显示上一张照片
        function showPrevPhoto() {
            if (currentPhotoIndex > 0) {
                currentPhotoIndex--;
                document.getElementById('modal-photo').src = currentPhotos[currentPhotoIndex];
            }
        }
        
        // 保存楼盘信息
        function saveProject() {
            const project = {
                id: Date.now(),
                name: document.getElementById('project-name').value,
                traffic: document.getElementById('project-traffic').value,
                market: document.getElementById('project-market').value,
                business: document.getElementById('project-business').value,
                medical: document.getElementById('project-medical').value,
                primary: document.getElementById('project-primary').value,
                middle: document.getElementById('project-middle').value,
                peripheryRemark: document.getElementById('project-periphery-remark').value,
                builtYear: document.getElementById('project-built-year').value,
                greening: document.getElementById('project-greening').value,
                plotRatio: document.getElementById('project-plot-ratio').value,
                property: document.getElementById('project-property').value,
                parking: document.getElementById('project-parking').value,
                infoRemark: document.getElementById('project-info-remark').value,
                timestamp: new Date().toISOString()
            };
            
            if (!project.name) {
                showToast('请输入楼盘名称');
                return;
            }
            
            // 保存照片
            const previewContainer = document.getElementById('project-photos-preview');
            const photoPreviews = previewContainer.querySelectorAll('.photo-preview img');
            const photos = [];
            
            photoPreviews.forEach(preview => {
                photos.push(preview.src);
            });
            
            // 保存照片到本地存储
            if (photos.length > 0) {
                const projectPhotos = getLocalData('realEstateProjectPhotos') || [];
                projectPhotos.push({
                    projectId: project.id,
                    photos: photos
                });
                saveLocalData('realEstateProjectPhotos', projectPhotos);
            }
            
            const projects = getLocalData('realEstateProjects');
            projects.push(project);
            saveLocalData('realEstateProjects', projects);
            
            showToast('楼盘信息保存成功！');
            showPage('home-page');
            loadRecentRecords();
        }
        
        // 保存房源信息
        function saveHouse() {
            const house = {
                id: Date.now(),
                projectId: document.getElementById('house-project').value,
                projectName: document.getElementById('house-project').options[document.getElementById('house-project').selectedIndex].text,
                totalPrice: document.getElementById('house-total-price').value,
                area: document.getElementById('house-area').value,
                unitPrice: document.getElementById('house-unit-price').value,
                elevator: document.getElementById('house-elevator').value,
                floor: document.getElementById('house-floor').value,
                number: document.getElementById('house-number').value,
                layout: document.getElementById('house-layout').value,
                parking: document.getElementById('house-parking').value,
                orientation: document.getElementById('house-orientation').value,
                decoration: document.getElementById('house-decoration').value,
                infoRemark: document.getElementById('house-info-remark').value,
                deedTax: document.getElementById('house-deed-tax').value,
                propertyTax: document.getElementById('house-property-tax').value,
                vat: document.getElementById('house-vat').value,
                transactionRemark: document.getElementById('house-transaction-remark').value,
                timestamp: new Date().toISOString()
            };
            
            if (!house.projectId) {
                showToast('请选择所属楼盘');
                return;
            }
            
            if (!house.totalPrice || !house.area) {
                showToast('请填写总价和面积');
                return;
            }
            
            // 保存照片
            const previewContainer = document.getElementById('house-photos-preview');
            const photoPreviews = previewContainer.querySelectorAll('.photo-preview img');
            const photos = [];
            
            photoPreviews.forEach(preview => {
                photos.push(preview.src);
            });
            
            // 保存照片到本地存储
            if (photos.length > 0) {
                const housePhotos = getLocalData('realEstateHousePhotos') || [];
                housePhotos.push({
                    houseId: house.id,
                    photos: photos
                });
                saveLocalData('realEstateHousePhotos', housePhotos);
            }
            
            const houses = getLocalData('realEstateHouses');
            houses.push(house);
            saveLocalData('realEstateHouses', houses);
            
            showToast('房源信息保存成功！');
            showPage('home-page');
            loadRecentRecords();
        }
        
        // 加载楼盘下拉菜单选项
        function loadProjectOptions() {
            const projects = getLocalData('realEstateProjects');
            const select = document.getElementById('house-project');
            
            // 清空现有选项（保留第一个提示选项）
            while (select.options.length > 1) {
                select.remove(1);
            }
            
            // 添加新选项
            projects.forEach(project => {
                const option = document.createElement('option');
                option.value = project.id;
                option.textContent = project.name;
                select.appendChild(option);
            });
        }
        
        // 加载最近记录
        function loadRecentRecords() {
            const projects = getLocalData('realEstateProjects');
            const houses = getLocalData('realEstateHouses');
            const list = document.getElementById('recent-records-list');
            
            // 清空现有记录
            list.innerHTML = '';
            
            // 合并记录并按时间排序
            const allRecords = [...projects, ...houses]
                .sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp))
                .slice(0, 5);
            
            if (allRecords.length === 0) {
                list.innerHTML = '<li class="record-item" style="justify-content:center; color:#888;">暂无记录</li>';
                return;
            }
            
            // 添加记录到列表
            allRecords.forEach(record => {
                const li = document.createElement('li');
                li.className = 'record-item';
                
                // 添加数据属性以便点击时获取详细信息
                if (record.projectName) {
                    // 房源记录
                    li.setAttribute('data-id', record.id);
                    li.setAttribute('data-type', 'house');
                    li.innerHTML = `
                        <div class="record-icon">
                            <i class="fas fa-home"></i>
                        </div>
                        <div class="record-info">
                            <h4>${record.projectName} ${record.number || ''}</h4>
                            <p>${formatDate(record.timestamp)} 记录 | ${record.area || ''}㎡ ${record.layout || ''}</p>
                        </div>
                        <button class="delete-btn" onclick="confirmDelete('house', ${record.id}, event)">
                            <i class="fas fa-trash"></i>
                        </button>
                    `;
                } else {
                    // 楼盘记录
                    li.setAttribute('data-id', record.id);
                    li.setAttribute('data-type', 'project');
                    li.innerHTML = `
                        <div class="record-icon">
                            <i class="fas fa-building"></i>
                        </div>
                        <div class="record-info">
                            <h4>${record.name}</h4>
                            <p>${formatDate(record.timestamp)} 记录 | ${record.property || '楼盘信息'}</p>
                        </div>
                        <button class="delete-btn" onclick="confirmDelete('project', ${record.id}, event)">
                            <i class="fas fa-trash"></i>
                        </button>
                    `;
                }
                
                // 添加点击事件
                li.addEventListener('click', function(e) {
                    // 如果点击的是删除按钮，则不触发详情查看
                    if (e.target.closest('.delete-btn')) {
                        return;
                    }
                    
                    const id = this.getAttribute('data-id');
                    const type = this.getAttribute('data-type');
                    
                    if (type === 'project') {
                        showProjectDetail(id);
                    } else if (type === 'house') {
                        showHouseDetail(id);
                    }
                });
                
                list.appendChild(li);
            });
        }
        
        // 显示楼盘详情
        function showProjectDetail(projectId) {
            const projects = getLocalData('realEstateProjects');
            const project = projects.find(p => p.id == projectId);
            
            if (project) {
                currentDetailId = projectId;
                
                // 填充楼盘详情数据
                document.getElementById('project-detail-name').textContent = project.name;
                document.getElementById('project-detail-built-year').textContent = project.builtYear || '--';
                document.getElementById('project-detail-greening').textContent = project.greening || '--';
                document.getElementById('project-detail-plot-ratio').textContent = project.plotRatio || '--';
                document.getElementById('project-detail-property').textContent = project.property || '--';
                document.getElementById('project-detail-parking').textContent = project.parking || '--';
                document.getElementById('project-detail-info-remark').textContent = project.infoRemark || '--';
                document.getElementById('project-detail-traffic').textContent = project.traffic || '--';
                document.getElementById('project-detail-market').textContent = project.market || '--';
                document.getElementById('project-detail-business').textContent = project.business || '--';
                document.getElementById('project-detail-medical').textContent = project.medical || '--';
                document.getElementById('project-detail-primary').textContent = project.primary || '--';
                document.getElementById('project-detail-middle').textContent = project.middle || '--';
                document.getElementById('project-detail-periphery-remark').textContent = project.peripheryRemark || '--';
                
                // 加载楼盘照片
                const photoContainer = document.getElementById('project-detail-photos');
                photoContainer.innerHTML = '';
                
                const projectPhotos = getLocalData('realEstateProjectPhotos') || [];
                const photos = projectPhotos.find(p => p.projectId == projectId)?.photos || [];
                
                if (photos.length === 0) {
                    photoContainer.innerHTML = '<div class="empty-state">暂无照片</div>';
                } else {
                    photos.forEach((photo, index) => {
                        const photoPreview = document.createElement('div');
                        photoPreview.className = 'photo-preview';
                        photoPreview.innerHTML = `<img src="${photo}" alt="楼盘照片">`;
                        photoPreview.onclick = () => openPhotoModal(photos, index, projectId, 'project');
                        photoContainer.appendChild(photoPreview);
                    });
                }
                
                // 更新头部标题
                document.querySelector('.header-title h1').textContent = project.name;
                document.querySelector('.header-title p').textContent = '楼盘详情';
                
                showPage('project-detail-page');
            }
        }
        
        // 显示房源详情
        function showHouseDetail(houseId) {
            const houses = getLocalData('realEstateHouses');
            const projects = getLocalData('realEstateProjects');
            const house = houses.find(h => h.id == houseId);
            
            if (house) {
                currentDetailId = houseId;
                
                // 填充房源详情数据
                document.getElementById('house-detail-project').textContent = house.projectName;
                document.getElementById('house-detail-number').textContent = house.number || '--';
                document.getElementById('house-detail-total-price').textContent = house.totalPrice ? `${house.totalPrice}万元` : '--';
                document.getElementById('house-detail-area').textContent = house.area ? `${house.area}㎡` : '--';
                document.getElementById('house-detail-unit-price').textContent = house.unitPrice || '--';
                document.getElementById('house-detail-layout').textContent = house.layout || '--';
                document.getElementById('house-detail-floor').textContent = house.floor || '--';
                document.getElementById('house-detail-orientation').textContent = house.orientation || '--';
                document.getElementById('house-detail-decoration').textContent = house.decoration || '--';
                document.getElementById('house-detail-elevator').textContent = house.elevator || '--';
                document.getElementById('house-detail-parking').textContent = house.parking || '--';
                document.getElementById('house-detail-info-remark').textContent = house.infoRemark || '--';
                document.getElementById('house-detail-deed-tax').textContent = house.deedTax || '--';
                document.getElementById('house-detail-property-tax').textContent = house.propertyTax || '--';
                document.getElementById('house-detail-vat').textContent = house.vat || '--';
                document.getElementById('house-detail-transaction-remark').textContent = house.transactionRemark || '--';
                
                // 加载房源照片
                const photoContainer = document.getElementById('house-detail-photos');
                photoContainer.innerHTML = '';
                
                const housePhotos = getLocalData('realEstateHousePhotos') || [];
                const photos = housePhotos.find(p => p.houseId == houseId)?.photos || [];
                
                if (photos.length === 0) {
                    photoContainer.innerHTML = '<div class="empty-state">暂无照片</div>';
                } else {
                    photos.forEach((photo, index) => {
                        const photoPreview = document.createElement('div');
                        photoPreview.className = 'photo-preview';
                        photoPreview.innerHTML = `<img src="${photo}" alt="房源照片">`;
                        photoPreview.onclick = () => openPhotoModal(photos, index, houseId, 'house');
                        photoContainer.appendChild(photoPreview);
                    });
                }
                
                // 更新头部标题
                document.querySelector('.header-title h1').textContent = house.projectName;
                document.querySelector('.header-title p').textContent = house.number ? `房源详情 - ${house.number}` : '房源详情';
                
                showPage('house-detail-page');
            }
        }
        
        // 更新统计信息
        function updateStats() {
            const projects = getLocalData('realEstateProjects');
            const houses = getLocalData('realEstateHouses');
            
            document.getElementById('project-count').textContent = projects.length;
            document.getElementById('house-count').textContent = houses.length;
        }
        
        // 格式化日期
        function formatDate(dateString) {
            const date = new Date(dateString);
            return `${date.getFullYear()}-${(date.getMonth() + 1).toString().padStart(2, '0')}-${date.getDate().toString().padStart(2, '0')}`;
        }
        
        // 自动计算单价
        document.getElementById('house-total-price').addEventListener('input', calculateUnitPrice);
        document.getElementById('house-area').addEventListener('input', calculateUnitPrice);
        
        function calculateUnitPrice() {
            const totalPrice = parseFloat(document.getElementById('house-total-price').value);
            const area = parseFloat(document.getElementById('house-area').value);
            
            if (totalPrice && area) {
                const unitPrice = (totalPrice * 10000 / area).toFixed(2);
                document.getElementById('house-unit-price').value = unitPrice + '元/㎡';
            } else {
                document.getElementById('house-unit-price').value = '';
            }
        }
        
        // 导出数据为Excel
        function exportData() {
            const projects = getLocalData('realEstateProjects');
            const houses = getLocalData('realEstateHouses');
            
            // 创建工作簿
            const wb = XLSX.utils.book_new();
            
            // 创建楼盘工作表
            const projectData = projects.map(project => {
                return {
                    '楼盘名称': project.name,
                    '交通': project.traffic,
                    '超市': project.market,
                    '商业': project.business,
                    '医疗': project.medical,
                    '小学': project.primary,
                    '中学': project.middle,
                    '周边备注': project.peripheryRemark,
                    '建成时间': project.builtYear,
                    '绿化率': project.greening,
                    '容积率': project.plotRatio,
                    '物业公司': project.property,
                    '车位情况': project.parking,
                    '楼盘备注': project.infoRemark,
                    '记录时间': formatDate(project.timestamp)
                };
            });
            
            const projectWs = XLSX.utils.json_to_sheet(projectData);
            XLSX.utils.book_append_sheet(wb, projectWs, "楼盘信息");
            
            // 创建房源工作表
            const houseData = houses.map(house => {
                return {
                    '所属楼盘': house.projectName,
                    '总价(万元)': house.totalPrice,
                    '面积(㎡)': house.area,
                    '单价(元/㎡)': house.unitPrice,
                    '电梯': house.elevator,
                    '楼层': house.floor,
                    '房号': house.number,
                    '户型': house.layout,
                    '车位': house.parking,
                    '朝向': house.orientation,
                    '装修': house.decoration,
                    '房源备注': house.infoRemark,
                    '契税': house.deedTax,
                    '房产税': house.propertyTax,
                    '增值税': house.vat,
                    '交易备注': house.transactionRemark,
                    '记录时间': formatDate(house.timestamp)
                };
            });
            
            const houseWs = XLSX.utils.json_to_sheet(houseData);
            XLSX.utils.book_append_sheet(wb, houseWs, "房源信息");
            
            // 导出Excel文件
            XLSX.writeFile(wb, "看房记录数据.xlsx");
            
            showToast('Excel数据导出成功！');
        }
        
        // 加载楼盘记录用于管理
        function loadProjectsForManagement() {
            const projects = getLocalData('realEstateProjects');
            const container = document.getElementById('projects-list-container');
            
            if (projects.length === 0) {
                container.innerHTML = '<div class="empty-state"><i class="fas fa-building"></i><p>暂无楼盘记录</p></div>';
                return;
            }
            
            let tableHTML = `
                <table class="record-table">
                    <thead>
                        <tr>
                            <th>楼盘名称</th>
                            <th>建成时间</th>
                            <th>记录时间</th>
                            <th>操作</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            projects.forEach(project => {
                tableHTML += `
                    <tr>
                        <td>${project.name}</td>
                        <td>${project.builtYear || '--'}</td>
                        <td>${formatDate(project.timestamp)}</td>
                        <td>
                            <button class="action-btn" onclick="showProjectDetail(${project.id})">
                                <i class="fas fa-eye"></i> 查看
                            </button>
                            <button class="action-btn delete-action" onclick="confirmDelete('project', ${project.id}, event)">
                                <i class="fas fa-trash"></i> 删除
                            </button>
                        </td>
                    </tr>
                `;
            });
            
            tableHTML += `
                    </tbody>
                </table>
            `;
            
            container.innerHTML = tableHTML;
        }
        
        // 加载房源记录用于管理
        function loadHousesForManagement() {
            const houses = getLocalData('realEstateHouses');
            const container = document.getElementById('houses-list-container');
            
            if (houses.length === 0) {
                container.innerHTML = '<div class="empty-state"><i class="fas fa-home"></i><p>暂无房源记录</p></div>';
                return;
            }
            
            let tableHTML = `
                <table class="record-table">
                    <thead>
                        <tr>
                            <th>所属楼盘</th>
                            <th>房号</th>
                            <th>总价(万元)</th>
                            <th>记录时间</th>
                            <th>操作</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            houses.forEach(house => {
                tableHTML += `
                    <tr>
                        <td>${house.projectName}</td>
                        <td>${house.number || '--'}</td>
                        <td>${house.totalPrice || '--'}</td>
                        <td>${formatDate(house.timestamp)}</td>
                        <td>
                            <button class="action-btn" onclick="showHouseDetail(${house.id})">
                                <i class="fas fa-eye"></i> 查看
                            </button>
                            <button class="action-btn delete-action" onclick="confirmDelete('house', ${house.id}, event)">
                                <i class="fas fa-trash"></i> 删除
                            </button>
                        </td>
                    </tr>
                `;
            });
            
            tableHTML += `
                    </tbody>
                </table>
            `;
            
            container.innerHTML = tableHTML;
        }
        
        // 确认删除
        function confirmDelete(type, id, event) {
            if (event) {
                event.stopPropagation(); // 防止事件冒泡
            }
            
            currentDeleteType = type;
            currentDeleteId = id;
            
            let message = "您确定要删除这条记录吗？此操作不可恢复。";
            if (type === 'project') {
                const projects = getLocalData('realEstateProjects');
                const project = projects.find(p => p.id == id);
                if (project) {
                    message = `确定要删除楼盘 "${project.name}" 吗？此操作不可恢复。`;
                }
            } else if (type === 'house') {
                const houses = getLocalData('realEstateHouses');
                const house = houses.find(h => h.id == id);
                if (house) {
                    message = `确定要删除房源 "${house.projectName} ${house.number || ''}" 吗？此操作不可恢复。`;
                }
            }
            
            document.getElementById('delete-message').textContent = message;
            document.getElementById('delete-modal').classList.add('active');
        }
        
        // 关闭删除确认模态框
        function closeDeleteModal() {
            document.getElementById('delete-modal').classList.remove('active');
        }
        
        // 执行删除操作
        function deleteRecord() {
            if (currentDeleteType === 'project') {
                // 删除楼盘
                let projects = getLocalData('realEstateProjects');
                projects = projects.filter(p => p.id != currentDeleteId);
                saveLocalData('realEstateProjects', projects);
                
                // 删除关联的照片
                let projectPhotos = getLocalData('realEstateProjectPhotos') || [];
                projectPhotos = projectPhotos.filter(p => p.projectId != currentDeleteId);
                saveLocalData('realEstateProjectPhotos', projectPhotos);
                
                // 删除关联的房源
                let houses = getLocalData('realEstateHouses');
                houses = houses.filter(h => h.projectId != currentDeleteId);
                saveLocalData('realEstateHouses', houses);
                
                showToast('楼盘已删除');
                
            } else if (currentDeleteType === 'house') {
                // 删除房源
                let houses = getLocalData('realEstateHouses');
                houses = houses.filter(h => h.id != currentDeleteId);
                saveLocalData('realEstateHouses', houses);
                
                // 删除关联的照片
                let housePhotos = getLocalData('realEstateHousePhotos') || [];
                housePhotos = housePhotos.filter(p => p.houseId != currentDeleteId);
                saveLocalData('realEstateHousePhotos', housePhotos);
                
                showToast('房源已删除');
            }
            
            // 关闭模态框
            closeDeleteModal();
            
            // 更新UI
            loadRecentRecords();
            updateStats();
            
            // 如果当前在详情页，返回首页
            if (document.getElementById('project-detail-page').classList.contains('active') || 
                document.getElementById('house-detail-page').classList.contains('active')) {
                showPage('home-page');
            }
            
            // 如果当前在管理页面，刷新列表
            if (document.getElementById('manage-projects-page').classList.contains('active')) {
                loadProjectsForManagement();
            } else if (document.getElementById('manage-houses-page').classList.contains('active')) {
                loadHousesForManagement();
            }
        }
        
        // 清除数据
        function clearData() {
            if (confirm('确定要清除所有数据吗？此操作不可恢复！')) {
                localStorage.removeItem('realEstateProjects');
                localStorage.removeItem('realEstateHouses');
                localStorage.removeItem('realEstateProjectPhotos');
                localStorage.removeItem('realEstateHousePhotos');
                showToast('数据已清除');
                showPage('home-page');
                loadRecentRecords();
                updateStats();
            }
        }
        
        // 初始化
        window.onload = function() {
            loadRecentRecords();
            updateStats();
            
            // 添加照片上传事件监听
            document.getElementById('project-photo-input').addEventListener('change', function(e) {
                previewPhotos(e, 'project');
            });
            
            document.getElementById('house-photo-input').addEventListener('change', function(e) {
                previewPhotos(e, 'house');
            });
            
            // 设置删除确认按钮事件
            document.getElementById('confirm-delete-btn').addEventListener('click', deleteRecord);
            
            // 添加一些示例数据
            if (getLocalData('realEstateProjects').length === 0) {
                const exampleProjects = [
                    {
                        id: 1,
                        name: "绿城·翡翠园",
                        traffic: "地铁2号线、公交123路",
                        market: "沃尔玛超市",
                        business: "万达广场",
                        medical: "市第一医院",
                        primary: "实验小学",
                        middle: "实验中学",
                        peripheryRemark: "周边配套完善，生活便利",
                        builtYear: "2020年",
                        greening: "35%",
                        plotRatio: "2.5",
                        property: "绿城物业",
                        parking: "1:1.2",
                        infoRemark: "高档住宅小区",
                        timestamp: "2023-10-15T08:30:00Z"
                    },
                    {
                        id: 2,
                        name: "龙湖·天宸原著",
                        traffic: "地铁3号线、公交456路",
                        market: "永辉超市",
                        business: "龙湖天街",
                        medical: "市第二医院",
                        primary: "育才小学",
                        middle: "育才中学",
                        peripheryRemark: "商业配套齐全",
                        builtYear: "2019年",
                        greening: "40%",
                        plotRatio: "2.2",
                        property: "龙湖物业",
                        parking: "1:1.5",
                        infoRemark: "高端改善型住宅",
                        timestamp: "2023-10-10T10:15:00Z"
                    }
                ];
                
                const exampleHouses = [
                    {
                        id: 101,
                        projectId: 1,
                        projectName: "绿城·翡翠园",
                        totalPrice: 420,
                        area: 89,
                        unitPrice: "47191元/㎡",
                        elevator: "有电梯",
                        floor: "12/28",
                        number: "3栋1202",
                        layout: "三室两厅一卫",
                        parking: "无车位",
                        orientation: "南向",
                        decoration: "精装",
                        infoRemark: "满五唯一，采光好",
                        deedTax: "4.2万",
                        propertyTax: "0",
                        vat: "0",
                        transactionRemark: "业主急售",
                        timestamp: "2023-10-16T09:30:00Z"
                    },
                    {
                        id: 102,
                        projectId: 2,
                        projectName: "龙湖·天宸原著",
                        totalPrice: 580,
                        area: 110,
                        unitPrice: "52727元/㎡",
                        elevator: "有电梯",
                        floor: "15/32",
                        number: "5栋1503",
                        layout: "四室两厅两卫",
                        parking: "含车位",
                        orientation: "南北通透",
                        decoration: "豪装",
                        infoRemark: "中央空调，地暖",
                        deedTax: "5.8万",
                        propertyTax: "0",
                        vat: "0",
                        transactionRemark: "可议价",
                        timestamp: "2023-10-12T14:20:00Z"
                    }
                ];
                
                saveLocalData('realEstateProjects', exampleProjects);
                saveLocalData('realEstateHouses', exampleHouses);
                loadRecentRecords();
                updateStats();
            }
        };
    </script>
</body>
</html>
