# Physics-Islands
这是一个介绍物理学的网站。🐿️
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>物理学小岛 - 公式思维导图</title>
    <style>
        /* 重置和基础样式 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        :root {
            --mechanics-color: #4CAF50;
            --electromagnetism-color: #2196F3;
            --thermodynamics-color: #F44336;
            --quantum-color: #9C27B0;
            --relativity-color: #FF9800;
            --ocean-dark: #1a237e;
            --ocean-light: #4fc3f7;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background: linear-gradient(135deg, var(--ocean-dark) 0%, var(--ocean-light) 100%);
            color: white;
            min-height: 100vh;
            padding: 20px;
        }
        
        /* 标题区域 */
        .header {
            text-align: center;
            padding: 30px 20px;
            margin-bottom: 20px;
        }
        
        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
        }
        
        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }
        
        /* 分类选择器 */
        .category-selector {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 40px;
            padding: 0 20px;
        }
        
        .category-btn {
            background: rgba(255, 255, 255, 0.15);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 20px;
            padding: 15px 25px;
            color: white;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
            min-width: 120px;
        }
        
        .category-btn:hover {
            background: rgba(255, 255, 255, 0.25);
            transform: translateY(-3px);
        }
        
        .category-btn.active {
            background: rgba(255, 255, 255, 0.3);
            border-color: white;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
        }
        
        .category-icon {
            font-size: 2em;
        }
        
        /* 主内容区域 */
        .content-area {
            display: flex;
            flex-direction: column;
            max-width: 1400px;
            margin: 0 auto;
            gap: 30px;
        }
        
        @media (min-width: 992px) {
            .content-area {
                flex-direction: row;
            }
        }
        
        /* 岛屿地图区域 */
        .island-map {
            flex: 3;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 25px;
            backdrop-filter: blur(10px);
            padding: 30px;
            min-height: 600px;
            position: relative;
            overflow: hidden;
        }
        
        .island-bg {
            position: absolute;
            border-radius: 50%;
            opacity: 0.2;
            transition: all 0.5s ease;
        }
        
        .island-bg.active {
            opacity: 0.4;
        }
        
        /* 公式节点 */
        .formula-node {
            position: absolute;
            cursor: pointer;
            z-index: 10;
            transition: all 0.3s ease;
        }
        
        .formula-circle {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            font-weight: bold;
            color: white;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
            border: 3px solid rgba(255, 255, 255, 0.8);
        }
        
        .formula-circle:hover {
            transform: scale(1.15);
            box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
        }
        
        .formula-name {
            position: absolute;
            top: calc(100% + 8px);
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 6px 12px;
            border-radius: 10px;
            font-size: 0.9em;
            white-space: nowrap;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .formula-node:hover .formula-name {
            opacity: 1;
        }
        
        /* 连接线 */
        .connection {
            position: absolute;
            height: 2px;
            background: rgba(255, 255, 255, 0.5);
            transform-origin: left center;
            z-index: 5;
        }
        
        /* 详情面板 */
        .detail-panel {
            flex: 1;
            background: rgba(0, 0, 0, 0.7);
            border-radius: 25px;
            padding: 30px;
            backdrop-filter: blur(10px);
            min-width: 300px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .detail-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .detail-category {
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: 600;
        }
        
        .formula-display {
            font-size: 3em;
            text-align: center;
            margin: 25px 0;
            font-family: 'Courier New', monospace;
            font-weight: bold;
        }
        
        .formula-description {
            font-size: 1.1em;
            line-height: 1.6;
            margin-bottom: 25px;
            opacity: 0.9;
        }
        
        .connections-section h4 {
            margin-bottom: 15px;
            font-size: 1.1em;
        }
        
        .connection-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .connection-tag {
            background: rgba(255, 255, 255, 0.15);
            padding: 8px 15px;
            border-radius: 15px;
            font-size: 0.9em;
        }
        
        /* 搜索框 */
        .search-container {
            margin-bottom: 30px;
            padding: 0 20px;
        }
        
        .search-box {
            width: 100%;
            max-width: 400px;
            margin: 0 auto;
            display: flex;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 25px;
            padding: 15px 20px;
            border: 2px solid rgba(255, 255, 255, 0.3);
        }
        
        .search-box input {
            flex: 1;
            background: transparent;
            border: none;
            color: white;
            font-size: 1.1em;
            outline: none;
        }
        
        .search-box input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }
        
        .search-icon {
            font-size: 1.2em;
            opacity: 0.7;
        }
        
        /* 响应式调整 */
        @media (max-width: 991px) {
            .header h1 {
                font-size: 2.2em;
            }
            
            .category-btn {
                padding: 12px 20px;
                min-width: 100px;
            }
            
            .island-map {
                min-height: 500px;
            }
            
            .formula-circle {
                width: 60px;
                height: 60px;
                font-size: 1em;
            }
        }
        
        @media (max-width: 576px) {
            .header h1 {
                font-size: 1.8em;
            }
            
            .category-selector {
                gap: 10px;
            }
            
            .category-btn {
                padding: 10px 15px;
                min-width: 90px;
                font-size: 0.9em;
            }
            
            .formula-circle {
                width: 50px;
                height: 50px;
                font-size: 0.9em;
            }
            
            .formula-display {
                font-size: 2.2em;
            }
        }
        
        /* 动画 */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease forwards;
        }
    </style>
</head>
<body>
    <!-- 标题区域 -->
    <div class="header">
        <h1>🏝️ 物理学小岛</h1>
        <p>探索公式之间的奇妙联系，发现物理学的统一之美</p>
    </div>
    
    <!-- 搜索框 -->
    <div class="search-container">
        <div class="search-box">
            <div class="search-icon">🔍</div>
            <input type="text" id="searchInput" placeholder="搜索公式或概念...">
        </div>
    </div>
    
    <!-- 分类选择器 -->
    <div class="category-selector">
        <div class="category-btn active" data-category="mechanics">
            <div class="category-icon">⚙️</div>
            <div>力学</div>
        </div>
        <div class="category-btn" data-category="electromagnetism">
            <div class="category-icon">🧲</div>
            <div>电磁学</div>
        </div>
        <div class="category-btn" data-category="thermodynamics">
            <div class="category-icon">🔥</div>
            <div>热力学</div>
        </div>
        <div class="category-btn" data-category="quantum">
            <div class="category-icon">⚛️</div>
            <div>量子物理</div>
        </div>
        <div class="category-btn" data-category="relativity">
            <div class="category-icon">🌀</div>
            <div>相对论</div>
        </div>
    </div>
    
    <!-- 主内容区域 -->
    <div class="content-area">
        <!-- 岛屿地图区域 -->
        <div class="island-map" id="islandMap">
            <!-- 岛屿背景将通过JavaScript动态创建 -->
            <!-- 公式节点将通过JavaScript动态创建 -->
            <!-- 连接线将通过JavaScript动态创建 -->
        </div>
        
        <!-- 详情面板 -->
        <div class="detail-panel" id="detailPanel">
            <div class="detail-header">
                <h2 id="detailTitle">选择一个公式</h2>
                <div class="detail-category" id="detailCategory" style="display:none;"></div>
            </div>
            
            <div id="formulaContent">
                <p style="text-align: center; opacity: 0.8; margin-top: 50px;">
                    点击左侧的公式节点查看详细信息
                </p>
            </div>
        </div>
    </div>
    
    <script>
        // 物理学数据模型
        const physicsData = {
            categories: {
                mechanics: {
                    name: "力学",
                    icon: "⚙️",
                    color: "var(--mechanics-color)",
                    description: "研究物体运动和力的关系，包括牛顿定律、动量、能量等。",
                    position: { x: 300, y: 250, radius: 200 }
                },
                electromagnetism: {
                    name: "电磁学",
                    icon: "🧲",
                    color: "var(--electromagnetism-color)",
                    description: "研究电荷、电场、磁场及其相互作用，包括麦克斯韦方程组。",
                    position: { x: 700, y: 150, radius: 180 }
                },
                thermodynamics: {
                    name: "热力学",
                    icon: "🔥",
                    color: "var(--thermodynamics-color)",
                    description: "研究热现象和能量转换，包括热力学定律和统计物理。",
                    position: { x: 200, y: 450, radius: 160 }
                },
                quantum: {
                    name: "量子物理",
                    icon: "⚛️",
                    color: "var(--quantum-color)",
                    description: "微观世界的物理学，包括波粒二象性、量子态和不确定性原理。",
                    position: { x: 800, y: 400, radius: 170 }
                },
                relativity: {
                    name: "相对论",
                    icon: "🌀",
                    color: "var(--relativity-color)",
                    description: "研究高速运动物体和引力场的物理学，包括狭义和广义相对论。",
                    position: { x: 500, y: 500, radius: 150 }
                }
            },
            
            formulas: [
                // 力学公式
                {
                    id: "newton-second",
                    name: "牛顿第二定律",
                    formula: "F = ma",
                    description: "力等于质量乘以加速度，是经典力学的核心公式。描述了力如何改变物体的运动状态。",
                    category: "mechanics",
                    connections: ["动量定理", "动能定理"],
                    position: { x: 0.3, y: 0.4 }, // 相对于岛屿中心的相对位置
                    importance: 5 // 重要性级别（1-5）
                },
                {
                    id: "momentum",
                    name: "动量定理",
                    formula: "p = mv",
                    description: "动量等于质量乘以速度，是描述物体运动状态的物理量。动量守恒是物理学的基本守恒定律之一。",
                    category: "mechanics",
                    connections: ["牛顿第二定律", "动能定理", "冲量定理"],
                    position: { x: 0.6, y: 0.2 },
                    importance: 4
                },
                {
                    id: "kinetic-energy",
                    name: "动能定理",
                    formula: "E_k = ½mv²",
                    description: "物体的动能等于质量乘以速度平方的一半。描述物体由于运动而具有的能量。",
                    category: "mechanics",
                    connections: ["牛顿第二定律", "动量定理"],
                    position: { x: 0.4, y: 0.7 },
                    importance: 4
                },
                
                // 电磁学公式
                {
                    id: "coulombs-law",
                    name: "库仑定律",
                    formula: "F = k·q₁q₂/r²",
                    description: "两点电荷之间的作用力与电荷量的乘积成正比，与距离平方成反比。是静电学的基础。",
                    category: "electromagnetism",
                    connections: ["电场强度", "高斯定律"],
                    position: { x: 0.3, y: 0.3 },
                    importance: 5
                },
                {
                    id: "ohms-law",
                    name: "欧姆定律",
                    formula: "V = IR",
                    description: "导体两端的电压与通过导体的电流成正比，比例系数为电阻。是电路理论的基本定律。",
                    category: "electromagnetism",
                    connections: ["电功率", "基尔霍夫定律"],
                    position: { x: 0.7, y: 0.5 },
                    importance: 5
                },
                {
                    id: "maxwell-equations",
                    name: "麦克斯韦方程组",
                    formula: "∇·E = ρ/ε₀",
                    description: "电磁场的基本方程，统一了电学和磁学，预言了电磁波的存在。",
                    category: "electromagnetism",
                    connections: ["库仑定律", "法拉第定律"],
                    position: { x: 0.5, y: 0.8 },
                    importance: 5
                },
                
                // 热力学公式
                {
                    id: "ideal-gas",
                    name: "理想气体状态方程",
                    formula: "PV = nRT",
                    description: "描述理想气体状态的基本方程，将压强、体积、物质的量和温度联系起来。",
                    category: "thermodynamics",
                    connections: ["玻尔兹曼熵公式"],
                    position: { x: 0.5, y: 0.5 },
                    importance: 5
                },
                {
                    id: "first-law",
                    name: "热力学第一定律",
                    formula: "ΔU = Q - W",
                    description: "能量守恒定律在热力学中的表达：系统内能的增加等于吸收的热量减去对外做的功。",
                    category: "thermodynamics",
                    connections: ["理想气体状态方程"],
                    position: { x: 0.2, y: 0.7 },
                    importance: 5
                },
                
                // 量子物理公式
                {
                    id: "planck",
                    name: "普朗克公式",
                    formula: "E = hf",
                    description: "能量等于普朗克常数乘以频率，是量子物理的奠基性公式，揭示了能量的量子化。",
                    category: "quantum",
                    connections: ["德布罗意关系", "薛定谔方程"],
                    position: { x: 0.4, y: 0.3 },
                    importance: 5
                },
                {
                    id: "schrodinger",
                    name: "薛定谔方程",
                    formula: "iℏ∂/∂t|Ψ⟩ = Ĥ|Ψ⟩",
                    description: "描述量子系统演化的基本方程，是量子力学的核心。",
                    category: "quantum",
                    connections: ["普朗克公式", "海森堡不确定性原理"],
                    position: { x: 0.7, y: 0.6 },
                    importance: 5
                },
                
                // 相对论公式
                {
                    id: "emc2",
                    name: "质能方程",
                    formula: "E = mc²",
                    description: "质量和能量等价，是狭义相对论的核心公式。揭示了物质蕴含的巨大能量。",
                    category: "relativity",
                    connections: ["洛伦兹变换"],
                    position: { x: 0.5, y: 0.5 },
                    importance: 5
                },
                {
                    id: "lorentz",
                    name: "洛伦兹变换",
                    formula: "t' = γ(t - vx/c²)",
                    description: "狭义相对论中不同惯性参考系之间的坐标变换，是相对论时空观的基础。",
                    category: "relativity",
                    connections: ["质能方程"],
                    position: { x: 0.3, y: 0.7 },
                    importance: 4
                }
            ]
        };
        
        // 当前状态
        let currentCategory = "mechanics";
        let selectedFormula = null;
        let allFormulas = [];
        
        // 初始化函数
        function init() {
            createIslandBackgrounds();
            createFormulaNodes();
            setupEventListeners();
            showCategory(currentCategory);
        }
        
        // 创建岛屿背景
        function createIslandBackgrounds() {
            const islandMap = document.getElementById('islandMap');
            
            for (const [categoryId, category] of Object.entries(physicsData.categories)) {
                const islandBg = document.createElement('div');
                islandBg.className = 'island-bg';
                islandBg.id = `island-${categoryId}`;
                islandBg.style.width = `${category.position.radius * 2}px`;
                islandBg.style.height = `${category.position.radius * 2}px`;
                islandBg.style.left = `${category.position.x - category.position.radius}px`;
                islandBg.style.top = `${category.position.y - category.position.radius}px`;
                islandBg.style.backgroundColor = category.color;
                
                islandMap.appendChild(islandBg);
            }
        }
        
        // 创建公式节点
        function createFormulaNodes() {
            const islandMap = document.getElementById('islandMap');
            
            physicsData.formulas.forEach(formula => {
                const category = physicsData.categories[formula.category];
                
                // 计算绝对位置
                const absoluteX = category.position.x + (formula.position.x - 0.5) * category.position.radius * 1.5;
                const absoluteY = category.position.y + (formula.position.y - 0.5) * category.position.radius * 1.5;
                
                // 创建节点容器
                const node = document.createElement('div');
                node.className = 'formula-node fade-in';
                node.id = `node-${formula.id}`;
                node.style.left = `${absoluteX}px`;
                node.style.top = `${absoluteY}px`;
                node.dataset.formulaId = formula.id;
                node.dataset.category = formula.category;
                
                // 创建公式圆圈
                const circle = document.createElement('div');
                circle.className = 'formula-circle';
                circle.style.backgroundColor = category.color;
                circle.textContent = formula.formula;
                
                // 创建公式名称标签
                const nameTag = document.createElement('div');
                nameTag.className = 'formula-name';
                nameTag.textContent = formula.name;
                
                // 组装节点
                node.appendChild(circle);
                node.appendChild(nameTag);
                islandMap.appendChild(node);
                
                // 保存节点信息
                allFormulas.push({
                    element: node,
                    formula: formula,
                    category: formula.category,
                    x: absoluteX,
                    y: absoluteY
                });
            });
        }
        
        // 显示特定分类的公式
        function showCategory(categoryId) {
            // 更新分类按钮状态
            document.querySelectorAll('.category-btn').forEach(btn => {
                if (btn.dataset.category === categoryId) {
                    btn.classList.add('active');
                } else {
                    btn.classList.remove('active');
                }
            });
            
            // 更新岛屿背景
            document.querySelectorAll('.island-bg').forEach(island => {
                if (island.id === `island-${categoryId}`) {
                    island.classList.add('active');
                } else {
                    island.classList.remove('active');
                }
            });
            
            // 显示/隐藏公式节点
            allFormulas.forEach(item => {
                if (item.category === categoryId) {
                    item.element.style.display = 'block';
                    item.element.classList.add('fade-in');
                } else {
                    item.element.style.display = 'none';
                }
            });
            
            // 更新当前分类
            currentCategory = categoryId;
            
            // 清除选中的公式
            selectedFormula = null;
            updateDetailPanel();
        }
        
        // 选择公式
        function selectFormula(formulaId) {
            const formula = physicsData.formulas.find(f => f.id === formulaId);
            if (!formula) return;
            
            selectedFormula = formula;
            
            // 移除之前的高亮
            document.querySelectorAll('.formula-circle').forEach(circle => {
                circle.classList.remove('pulse');
            });
            
            // 高亮当前公式
            const selectedNode = document.getElementById(`node-${formulaId}`);
            if (selectedNode) {
                const circle = selectedNode.querySelector('.formula-circle');
                circle.classList.add('pulse');
            }
            
            // 显示对应的分类
            if (formula.category !== currentCategory) {
                showCategory(formula.category);
            }
            
            // 更新详情面板
            updateDetailPanel();
        }
        
        // 更新详情面板
        function updateDetailPanel() {
            const detailPanel = document.getElementById('detailPanel');
            const detailTitle = document.getElementById('detailTitle');
            const detailCategory = document.getElementById('detailCategory');
            const formulaContent = document.getElementById('formulaContent');
            
            if (!selectedFormula) {
                detailTitle.textContent = "选择一个公式";
                detailCategory.style.display = 'none';
                formulaContent.innerHTML = `
                    <p style="text-align: center; opacity: 0.8; margin-top: 50px;">
                        点击左侧的公式节点查看详细信息
                    </p>
                `;
                return;
            }
            
            const category = physicsData.categories[selectedFormula.category];
            
            // 更新标题和分类
            detailTitle.textContent = selectedFormula.name;
            detailCategory.textContent = category.name;
            detailCategory.style.backgroundColor = category.color;
            detailCategory.style.display = 'inline-block';
            
            // 更新公式内容
            formulaContent.innerHTML = `
                <div class="formula-display">${selectedFormula.formula}</div>
                <div class="formula-description">${selectedFormula.description}</div>
                
                <div class="connections-section">
                    <h4>相关公式</h4>
                    <div class="connection-tags">
                        ${selectedFormula.connections.map(conn => 
                            `<div class="connection-tag">${conn}</div>`
                        ).join('')}
                    </div>
                </div>
                
                <div style="margin-top: 30px; padding-top: 20px; border-top: 1px solid rgba(255,255,255,0.2);">
                    <h4>所属领域：${category.name}</h4>
                    <p style="margin-top: 10px; opacity: 0.9;">${category.description}</p>
                </div>
            `;
        }
        
        // 搜索功能
        function searchFormulas(query) {
            if (!query.trim()) {
                // 清空搜索，显示当前分类
                showCategory(currentCategory);
                return;
            }
            
            const lowerQuery = query.toLowerCase();
            
            // 显示所有公式节点
            allFormulas.forEach(item => {
                item.element.style.display = 'block';
            });
            
            // 隐藏不匹配的节点
            allFormulas.forEach(item => {
                const formula = item.formula;
                const matches = 
                    formula.name.toLowerCase().includes(lowerQuery) ||
                    formula.formula.toLowerCase().includes(lowerQuery) ||
                    formula.description.toLowerCase().includes(lowerQuery) ||
                    formula.category.toLowerCase().includes(lowerQuery);
                
                item.element.style.opacity = matches ? '1' : '0.2';
                item.element.style.pointerEvents = matches ? 'auto' : 'none';
            });
            
            // 更新详情面板
            if (selectedFormula) {
                const formulaMatches = 
                    selectedFormula.name.toLowerCase().includes(lowerQuery) ||
                    selectedFormula.formula.toLowerCase().includes(lowerQuery) ||
                    selectedFormula.description.toLowerCase().includes(lowerQuery) ||
                    selectedFormula.category.toLowerCase().includes(lowerQuery);
                
                if (!formulaMatches) {
                    selectedFormula = null;
                    updateDetailPanel();
                }
            }
        }
        
        // 设置事件监听器
        function setupEventListeners() {
            // 分类按钮点击事件
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const category = this.dataset.category;
                    showCategory(category);
                });
            });
            
            // 公式节点点击事件
            document.addEventListener('click', function(event) {
                let element = event.target;
                
                // 向上查找公式节点
                while (element && !element.classList.contains('formula-node')) {
                    element = element.parentElement;
                }
                
                if (element && element.classList.contains('formula-node')) {
                    const formulaId = element.dataset.formulaId;
                    selectFormula(formulaId);
                }
            });
            
            // 搜索输入事件
            const searchInput = document.getElementById('searchInput');
            searchInput.addEventListener('input', function() {
                searchFormulas(this.value);
            });
            
            // 键盘快捷键
            document.addEventListener('keydown', function(event) {
                // ESC键清除搜索
                if (event.key === 'Escape') {
                    searchInput.value = '';
                    searchFormulas('');
                    searchInput.focus();
                }
                
                // Ctrl+F聚焦搜索框
                if ((event.ctrlKey || event.metaKey) && event.key === 'f') {
                    event.preventDefault();
                    searchInput.focus();
                }
            });
            
            // 窗口大小变化时调整布局
            window.addEventListener('resize', function() {
                // 可以在这里添加响应式调整代码
            });
        }
        
        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', init);
        
        // 可选：添加一些初始动画
        setTimeout(() => {
            if (!selectedFormula) {
                // 随机选择一个初始公式
                const mechanicsFormulas = physicsData.formulas.filter(f => f.category === 'mechanics');
                if (mechanicsFormulas.length > 0) {
                    const randomFormula = mechanicsFormulas[Math.floor(Math.random() * mechanicsFormulas.length)];
                    selectFormula(randomFormula.id);
                }
            }
        }, 1000);
    </script>
</body>
</html>