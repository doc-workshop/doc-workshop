HTML 成果交付
==================

请按项目要求提交你所完成的文档。

.. raw:: html

    <!DOCTYPE html>
    <html lang="zh-CN">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>HTML主题检查工具</title>
        <style>
            body {
                font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                line-height: 1.6;
                max-width: 800px;
                margin: 0 auto;
                padding: 20px;
                color: #333;
                background-color: #f8f9fa;
            }
            h1 {
                color: #2c3e50;
                text-align: center;
                margin-bottom: 30px;
                border-bottom: 2px solid #3498db;
                padding-bottom: 10px;
            }
            .container {
                background-color: white;
                border-radius: 8px;
                padding: 25px;
                box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            }
            .upload-area {
                border: 2px dashed #3498db;
                border-radius: 5px;
                padding: 25px;
                text-align: center;
                margin-bottom: 20px;
                background-color: #f8fafc;
                transition: all 0.3s;
            }
            .upload-area:hover {
                background-color: #e8f4fc;
            }
            .upload-area p {
                margin: 0;
                color: #7f8c8d;
            }
            input[type="file"] {
                margin: 15px 0;
                padding: 8px;
                border: 1px solid #ddd;
                border-radius: 4px;
                width: 80%;
            }
            button {
                background-color: #3498db;
                color: white;
                border: none;
                padding: 12px 24px;
                border-radius: 4px;
                cursor: pointer;
                font-size: 16px;
                transition: background-color 0.3s;
            }
            button:hover {
                background-color: #2980b9;
            }
            button:disabled {
                background-color: #95a5a6;
                cursor: not-allowed;
            }
            .result-area {
                margin-top: 30px;
                display: none;
            }
            .success {
                color: #27ae60;
                font-weight: bold;
            }
            .error {
                color: #e74c3c;
                font-weight: bold;
            }
            .file-content {
                margin-top: 20px;
                background-color: #f8fafc;
                border-left: 4px solid #3498db;
                padding: 15px;
                overflow-x: auto;
                display: none;
                max-height: 300px;
                overflow-y: auto;
            }
            pre {
                white-space: pre-wrap;
                margin: 0;
                font-family: 'Consolas', 'Monaco', monospace;
                font-size: 14px;
            }
            /* 弹窗样式 */
            .modal {
                display: none;
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background-color: rgba(0, 0, 0, 0.7);
                z-index: 1000;
                justify-content: center;
                align-items: center;
            }
            .modal-content {
                background-color: white;
                padding: 40px;
                border-radius: 10px;
                text-align: center;
                box-shadow: 0 5px 25px rgba(0, 0, 0, 0.3);
                max-width: 500px;
                width: 90%;
                animation: modalFadeIn 0.5s;
            }
            @keyframes modalFadeIn {
                from { opacity: 0; transform: translateY(-50px); }
                to { opacity: 1; transform: translateY(0); }
            }
            .modal h2 {
                color: #27ae60;
                margin-top: 0;
                font-size: 28px;
            }
            .modal p {
                font-size: 18px;
                margin: 20px 0;
            }
            .modal-button {
                background-color: #27ae60;
                color: white;
                border: none;
                padding: 12px 24px;
                border-radius: 4px;
                cursor: pointer;
                margin-top: 20px;
                font-size: 16px;
                transition: background-color 0.3s;
            }
            .modal-button:hover {
                background-color: #219653;
            }
            .info-table {
                width: 100%;
                border-collapse: collapse;
                margin-top: 20px;
                box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            }
            .info-table th, .info-table td {
                border: 1px solid #ddd;
                padding: 12px;
                text-align: left;
            }
            .info-table th {
                background-color: #f2f2f2;
                font-weight: bold;
            }
            .info-table tr:nth-child(even) {
                background-color: #f9f9f9;
            }
            .loading {
                display: none;
                text-align: center;
                margin: 20px 0;
            }
            .loading-spinner {
                border: 4px solid #f3f3f3;
                border-top: 4px solid #3498db;
                border-radius: 50%;
                width: 30px;
                height: 30px;
                animation: spin 1s linear infinite;
                margin: 0 auto;
            }
            @keyframes spin {
                0% { transform: rotate(0deg); }
                100% { transform: rotate(360deg); }
            }
            .author-source {
                font-size: 12px;
                color: #7f8c8d;
                margin-top: 5px;
            }
        </style>
    </head>
    <body>
        <div class="container">
            <h1>HTML主题检查工具</h1>
            
            <div class="upload-area">
                <p>请上传一个HTML文件进行检查</p>
                <input type="file" id="htmlFile" accept=".html,.htm">
                <br>
                <button id="checkButton" onclick="checkHTML()">检查主题</button>
            </div>
            
            <div class="loading" id="loadingIndicator">
                <div class="loading-spinner"></div>
                <p>正在分析文件...</p>
            </div>
            
            <div id="resultArea" class="result-area">
                <h2>检查结果</h2>
                <div id="resultMessage"></div>
                
                <h3>提取的信息</h3>
                <table class="info-table">
                    <thead>
                        <tr>
                            <th>信息类型</th>
                            <th>值</th>
                            <th>来源</th>
                        </tr>
                    </thead>
                    <tbody id="infoResults">
                        <!-- 结果将通过JavaScript填充 -->
                    </tbody>
                </table>
                
                <div id="fileContent" class="file-content">
                    <h3>文件内容预览</h3>
                    <pre id="contentPreview"></pre>
                </div>
            </div>
        </div>

        <!-- 成功弹窗 -->
        <div id="successModal" class="modal">
            <div class="modal-content">
                <h2>恭喜！</h2>
                <p id="congratsMessage"></p>
                <button class="modal-button" onclick="closeModal()">确定</button>
            </div>
        </div>

        <script>
            function checkHTML() {
                const fileInput = document.getElementById('htmlFile');
                const resultArea = document.getElementById('resultArea');
                const resultMessage = document.getElementById('resultMessage');
                const infoResults = document.getElementById('infoResults');
                const contentPreview = document.getElementById('contentPreview');
                const fileContentDiv = document.getElementById('fileContent');
                const congratsMessage = document.getElementById('congratsMessage');
                const loadingIndicator = document.getElementById('loadingIndicator');
                const checkButton = document.getElementById('checkButton');
                
                // 重置结果显示
                infoResults.innerHTML = '';
                resultMessage.innerHTML = '';
                resultArea.style.display = 'none';
                fileContentDiv.style.display = 'none';
                
                if (!fileInput.files || fileInput.files.length === 0) {
                    alert('请先选择一个HTML文件');
                    return;
                }
                
                // 显示加载指示器
                loadingIndicator.style.display = 'block';
                checkButton.disabled = true;
                
                const file = fileInput.files[0];
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    const content = e.target.result;
                    contentPreview.textContent = content;
                    
                    // 创建DOM解析器
                    const parser = new DOMParser();
                    const htmlDoc = parser.parseFromString(content, 'text/html');
                    
                    // 提取信息
                    const authorInfo = extractAuthorInfo(htmlDoc);
                    const theme = extractTheme(htmlDoc);
                    const title = extractTitle(htmlDoc);
                    
                    // 隐藏加载指示器
                    loadingIndicator.style.display = 'none';
                    checkButton.disabled = false;
                    
                    // 显示结果区域
                    resultArea.style.display = 'block';
                    fileContentDiv.style.display = 'block';
                    
                    // 显示提取的信息
                    infoResults.innerHTML = `
                        <tr>
                            <td>作者</td>
                            <td>${authorInfo.name || '未找到'}</td>
                            <td>${authorInfo.source || '未找到'}</td>
                        </tr>
                        <tr>
                            <td>主题</td>
                            <td>${theme || '未找到'}</td>
                            <td>${theme ? 'HTML/CSS' : '未找到'}</td>
                        </tr>
                        <tr>
                            <td>标题</td>
                            <td>${title || '未找到'}</td>
                            <td>${title ? '&lt;title&gt;标签' : '未找到'}</td>
                        </tr>
                    `;
                    
                    // 检查是否使用alabaster主题
                    if (theme && theme.toLowerCase().includes('alabaster')) {
                        resultMessage.innerHTML = `
                            <p class="success">✓ 文件使用了alabaster主题</p>
                        `;
                        
                        // 显示恭喜弹窗
                        setTimeout(() => {
                            const authorName = authorInfo.name || '未知作者';
                            congratsMessage.textContent = `恭喜 Author：${authorName} 完成任务`;
                            document.getElementById('successModal').style.display = 'flex';
                        }, 500);
                    } else {
                        resultMessage.innerHTML = `
                            <p class="error">✗ 文件未使用alabaster主题</p>
                            <p>当前主题: ${theme || '未找到主题信息'}</p>
                        `;
                    }
                };
                
                reader.onerror = function() {
                    // 隐藏加载指示器
                    loadingIndicator.style.display = 'none';
                    checkButton.disabled = false;
                    alert('读取文件时发生错误');
                };
                
                reader.readAsText(file);
            }
            
            // 提取作者信息（从contentinfo或footer）
            function extractAuthorInfo(htmlDoc) {
                let author = null;
                let source = null;
                
                // 1. 首先查找role="contentinfo"的元素
                const contentInfo = htmlDoc.querySelector('[role="contentinfo"]');
                if (contentInfo) {
                    author = extractAuthorFromElement(contentInfo);
                    if (author) {
                        source = 'contentinfo';
                        return { name: author, source: source };
                    }
                }
                
                // 2. 查找class包含"footer"的元素
                const footerElements = htmlDoc.querySelectorAll('[class*="footer"], [class*="Footer"]');
                for (const footer of footerElements) {
                    author = extractAuthorFromElement(footer);
                    if (author) {
                        source = 'footer';
                        return { name: author, source: source };
                    }
                }
                
                // 3. 查找footer标签
                const footerTag = htmlDoc.querySelector('footer');
                if (footerTag) {
                    author = extractAuthorFromElement(footerTag);
                    if (author) {
                        source = 'footer标签';
                        return { name: author, source: source };
                    }
                }
                
                // 4. 查找id包含"footer"的元素
                const footerById = htmlDoc.querySelector('[id*="footer"], [id*="Footer"]');
                if (footerById) {
                    author = extractAuthorFromElement(footerById);
                    if (author) {
                        source = 'footer ID';
                        return { name: author, source: source };
                    }
                }
                
                return { name: null, source: null };
            }
            
            // 从元素中提取作者信息
            function extractAuthorFromElement(element) {
                // 获取元素的文本内容
                const text = element.textContent.trim();
                
                // 尝试从文本中提取作者信息
                // 格式通常是: "Copyright 年份, 作者名" 或 "© 年份, 作者名"
                const copyrightPattern = /(?:©|Copyright|copyright)[\s\d.,–-]*,\s*([^.,]+)/i;
                const match = text.match(copyrightPattern);
                
                if (match && match[1]) {
                    return match[1].trim();
                }
                
                // 如果没有匹配到标准格式，尝试查找逗号后面的内容
                const commaIndex = text.lastIndexOf(',');
                if (commaIndex !== -1 && commaIndex < text.length - 1) {
                    const afterComma = text.substring(commaIndex + 1).trim();
                    // 确保逗号后面的内容不是纯数字（可能是年份）
                    if (!/^\d+$/.test(afterComma)) {
                        return afterComma;
                    }
                }
                
                return null;
            }
            
            // 提取主题信息
            function extractTheme(htmlDoc) {
                // 尝试从body的class中获取主题信息
                const bodyClasses = htmlDoc.body.className.split(' ');
                for (const cls of bodyClasses) {
                    if (cls.includes('theme') || cls.includes('alabaster')) {
                        return cls;
                    }
                }
                
                // 尝试从meta标签获取主题信息
                const metaTheme = htmlDoc.querySelector('meta[name="theme"]');
                if (metaTheme) return metaTheme.getAttribute('content');
                
                // 尝试从link标签获取主题信息
                const themeLinks = htmlDoc.querySelectorAll('link[rel*="style"]');
                for (const link of themeLinks) {
                    const href = link.getAttribute('href') || '';
                    if (href.includes('alabaster') || href.includes('theme')) {
                        return href;
                    }
                }
                
                return null;
            }
            
            // 提取标题信息
            function extractTitle(htmlDoc) {
                const title = htmlDoc.querySelector('title');
                return title ? title.textContent : null;
            }
            
            // 关闭弹窗
            function closeModal() {
                document.getElementById('successModal').style.display = 'none';
            }
            
            // 点击弹窗外部也可关闭
            window.onclick = function(event) {
                const modal = document.getElementById('successModal');
                if (event.target === modal) {
                    modal.style.display = 'none';
                }
            };
            
            // 拖放文件支持
            document.addEventListener('DOMContentLoaded', function() {
                const dropArea = document.querySelector('.upload-area');
                const fileInput = document.getElementById('htmlFile');
                
                // 防止默认拖放行为
                ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
                    dropArea.addEventListener(eventName, preventDefaults, false);
                });
                
                function preventDefaults(e) {
                    e.preventDefault();
                    e.stopPropagation();
                }
                
                // 高亮显示拖放区域
                ['dragenter', 'dragover'].forEach(eventName => {
                    dropArea.addEventListener(eventName, highlight, false);
                });
                
                ['dragleave', 'drop'].forEach(eventName => {
                    dropArea.addEventListener(eventName, unhighlight, false);
                });
                
                function highlight() {
                    dropArea.style.backgroundColor = '#e1f5fe';
                    dropArea.style.borderColor = '#03a9f4';
                }
                
                function unhighlight() {
                    dropArea.style.backgroundColor = '#f8fafc';
                    dropArea.style.borderColor = '#3498db';
                }
                
                // 处理文件拖放
                dropArea.addEventListener('drop', handleDrop, false);
                
                function handleDrop(e) {
                    const dt = e.dataTransfer;
                    const files = dt.files;
                    
                    if (files.length) {
                        fileInput.files = files;
                        
                        // 更新文件名显示
                        const fileNameDisplay = document.getElementById('fileName');
                        if (!fileNameDisplay) {
                            const p = document.createElement('p');
                            p.id = 'fileName';
                            p.style.marginTop = '10px';
                            p.style.fontSize = '14px';
                            dropArea.appendChild(p);
                        }
                        document.getElementById('fileName').textContent = `已选择文件: ${files[0].name}`;
                    }
                }
            });
        </script>
    </body>
    </html>