RST 成果交付
==================

请按项目要求提交你所完成的文档。

.. raw:: html

    <!DOCTYPE html>
    <html lang="zh-CN">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>RST语法检查工具</title>
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
            }
            button {
                background-color: #3498db;
                color: white;
                border: none;
                padding: 10px 20px;
                border-radius: 4px;
                cursor: pointer;
                font-size: 16px;
                transition: background-color 0.3s;
            }
            button:hover {
                background-color: #2980b9;
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
            .syntax-list {
                margin-top: 20px;
                border-collapse: collapse;
                width: 100%;
            }
            .syntax-list th, .syntax-list td {
                border: 1px solid #ddd;
                padding: 10px;
                text-align: left;
            }
            .syntax-list th {
                background-color: #f2f2f2;
            }
            .syntax-list tr:nth-child(even) {
                background-color: #f9f9f9;
            }
            .found {
                color: #27ae60;
            }
            .not-found {
                color: #e74c3c;
            }
            .file-content {
                margin-top: 20px;
                background-color: #f8fafc;
                border-left: 4px solid #3498db;
                padding: 15px;
                overflow-x: auto;
                display: none;
            }
            pre {
                white-space: pre-wrap;
                margin: 0;
            }
            /* 弹窗样式 */
            .modal {
                display: none;
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background-color: rgba(0, 0, 0, 0.5);
                z-index: 1000;
                justify-content: center;
                align-items: center;
            }
            .modal-content {
                background-color: white;
                padding: 30px;
                border-radius: 8px;
                text-align: center;
                box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
                max-width: 400px;
                width: 80%;
            }
            .modal h2 {
                color: #27ae60;
                margin-top: 0;
            }
            .modal-button {
                background-color: #27ae60;
                color: white;
                border: none;
                padding: 10px 20px;
                border-radius: 4px;
                cursor: pointer;
                margin-top: 20px;
                font-size: 16px;
            }
        </style>
    </head>
    <body>
        <div class="container">
            <h1>RST语法检查工具</h1>
            
            <div class="upload-area">
                <p>请上传一个RST文件进行检查</p>
                <input type="file" id="rstFile" accept=".rst,.txt">
                <br>
                <button onclick="checkRST()">检查语法</button>
            </div>
            
            <div id="resultArea" class="result-area">
                <h2>检查结果</h2>
                <div id="resultMessage"></div>
                
                <h3>语法元素使用情况</h3>
                <table class="syntax-list">
                    <thead>
                        <tr>
                            <th>语法元素</th>
                            <th>是否使用</th>
                            <th>示例</th>
                        </tr>
                    </thead>
                    <tbody id="syntaxResults">
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
                <p>恭喜你通过检查，请进行下一个任务。</p>
                <button class="modal-button" onclick="closeModal()">确定</button>
            </div>
        </div>

        <script>
            function checkRST() {
                const fileInput = document.getElementById('rstFile');
                const resultArea = document.getElementById('resultArea');
                const resultMessage = document.getElementById('resultMessage');
                const syntaxResults = document.getElementById('syntaxResults');
                const contentPreview = document.getElementById('contentPreview');
                const fileContentDiv = document.getElementById('fileContent');
                
                // 重置结果显示
                syntaxResults.innerHTML = '';
                resultMessage.innerHTML = '';
                resultArea.style.display = 'block';
                
                if (!fileInput.files || fileInput.files.length === 0) {
                    resultMessage.innerHTML = '<p class="error">请先选择一个RST文件</p>';
                    return;
                }
                
                const file = fileInput.files[0];
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    const content = e.target.result;
                    contentPreview.textContent = content;
                    fileContentDiv.style.display = 'block';
                    
                    // 检查各种RST语法元素
                    const checks = {
                        '段落': checkParagraphs(content),
                        '标题': checkHeadings(content),
                        '内联格式': checkInlineFormatting(content),
                        '列表': checkLists(content),
                        '代码块': checkCodeBlocks(content),
                        '表格': checkTables(content),
                        '链接': checkLinks(content),
                        '图像': checkImages(content)
                    };
                    
                    // 显示检查结果
                    let allChecksPassed = true;
                    let foundCount = 0;
                    
                    for (const [element, found] of Object.entries(checks)) {
                        const status = found ? '<span class="found">✓ 已使用</span>' : '<span class="not-found">✗ 未使用</span>';
                        let example = '';
                        
                        // 提供示例
                        switch(element) {
                            case '段落':
                                example = '连续文本行组成段落，段落间有空行';
                                break;
                            case '标题':
                                example = '= 标题 =<br>- 标题 -<br># 标题 #';
                                break;
                            case '内联格式':
                                example = '*强调*<br>**加粗**<br>``代码``';
                                break;
                            case '列表':
                                example = '- 项目符号<br>1. 编号<br>* 另一种符号';
                                break;
                            case '代码块':
                                example = '::<br><br>    缩进代码<br><br>或<br><br>.. code-block:: python';
                                break;
                            case '表格':
                                example = '===  ===<br>列1  列2<br>===  ===<br>数据1 数据2<br>===  ===';
                                break;
                            case '链接':
                                example = '`链接文本 <https://example.com>`_';
                                break;
                            case '图像':
                                example = '.. image:: image.png';
                                break;
                        }
                        
                        syntaxResults.innerHTML += `
                            <tr>
                                <td>${element}</td>
                                <td>${status}</td>
                                <td>${example}</td>
                            </tr>
                        `;
                        
                        if (found) foundCount++;
                        if (!found && ['段落', '标题', '内联格式'].includes(element)) {
                            allChecksPassed = false;
                        }
                    }
                    
                    // 显示总体结果
                    if (foundCount >= 3) { // 至少使用三种语法元素
                        resultMessage.innerHTML = `
                            <p class="success">✓ 文件包含了基本的RST语法元素</p>
                            <p>共检测到 ${foundCount} 种语法元素的使用</p>
                        `;
                        
                        // 检查通过，显示恭喜弹窗
                        setTimeout(() => {
                            document.getElementById('successModal').style.display = 'flex';
                        }, 500);
                    } else {
                        resultMessage.innerHTML = `
                            <p class="error">✗ 文件未包含足够的RST语法元素</p>
                            <p>仅检测到 ${foundCount} 种语法元素的使用，建议至少使用3种不同的语法元素</p>
                        `;
                    }
                };
                
                reader.readAsText(file);
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
            
            // 检查函数
            function checkParagraphs(content) {
                // 检查是否有多个段落（通过空行分隔）
                return (content.split(/\n\s*\n/).length > 1);
            }
            
            function checkHeadings(content) {
                // 检查标题（下划线或上划线标题）
                return /^(.*)\n[=\-~`:+_]{3,}$|^[=\-~`:+_]{3,}\n(.*)$/m.test(content);
            }
            
            function checkInlineFormatting(content) {
                // 检查内联格式：强调、加粗、代码等
                return /\*[^*\n]+\*|\*\*[^*\n]+\*\*|``[^`\n]+``/.test(content);
            }
            
            function checkLists(content) {
                // 检查项目符号或编号列表
                return /^[\*\-+]\s|\d+\.\s/.test(content);
            }
            
            function checkCodeBlocks(content) {
                // 检查代码块（缩进或代码块指令）
                return /^ {4,}\S|::\s*$|\.\.\s+code-block::/.test(content);
            }
            
            function checkTables(content) {
                // 检查简单表格
                return /^={2,}\s={2,}$|^\-{2,}\s\-{2,}$|^\+{2,}\+{2,}$/m.test(content);
            }
            
            function checkLinks(content) {
                // 检查链接
                return /`[^`]+<[^>]+>`_|\.\.\s+_`[^`]+`:\s+http/.test(content);
            }
            
            function checkImages(content) {
                // 检查图像
                return /\.\.\s+image::/.test(content);
            }
        </script>
    </body>
    </html>
