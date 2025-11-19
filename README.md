<!DOCTYPE html><html lang="en"><head>
    <meta charset="utf-8"/>
    <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
    <title>ACA Arcium Academy: A Visual Introduction</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Canela:wght@300;400;700&amp;family=Inter:wght@300;400;500;600;700&amp;display=swap" rel="stylesheet"/>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet"/>
    <script src="https://cdn.jsdelivr.net/npm/mermaid@10.6.1/dist/mermaid.min.js"></script>
    <style>
        :root {
            --primary: #1a1a2e;
            --secondary: #16213e;
            --accent: #0f3460;
            --highlight: #e94560;
            --neutral: #f8fafc;
            --base: #ffffff;
        }
        
        .font-canela { font-family: 'Canela', serif; }
        .font-inter { font-family: 'Inter', sans-serif; }
        
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(135deg, var(--neutral) 0%, #f1f5f9 100%);
            color: var(--primary);
            overflow-x: hidden;
        }
        
        .hero-gradient {
            background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 50%, var(--accent) 100%);
        }
        
        .text-gradient {
            background: linear-gradient(135deg, var(--highlight), #ff6b6b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .bento-grid {
            display: grid;
            grid-template-columns: 2fr 1fr;
            grid-template-rows: auto auto;
            gap: 2rem;
            height: 70vh;
        }
        
        .bento-main {
            grid-row: 1 / 3;
            position: relative;
            overflow: hidden;
            border-radius: 24px;
            background: linear-gradient(135deg, rgba(26, 26, 46, 0.95), rgba(15, 52, 96, 0.9));
        }
        
        .bento-side-1 {
            background: linear-gradient(135deg, rgba(233, 69, 96, 0.1), rgba(255, 107, 107, 0.05));
            border-radius: 16px;
            border: 1px solid rgba(233, 69, 96, 0.2);
            word-break: break-word;
        }
        
        .bento-side-2 {
            background: linear-gradient(135deg, rgba(26, 26, 46, 0.1), rgba(15, 52, 96, 0.05));
            border-radius: 16px;
            border: 1px solid rgba(26, 26, 46, 0.2);
            word-break: break-word;
        }
        
        .floating-element {
            position: absolute;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(5deg); }
        }
        
        .toc-fixed {
            position: fixed;
            top: 50%;
            left: 2rem;
            transform: translateY(-50%);
            width: 280px;
            max-height: 80vh;
            overflow-y: auto;
            z-index: 40;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 16px;
            border: 1px solid rgba(26, 26, 46, 0.1);
            padding: 1.5rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        
        .content-main {
            margin-left: 320px;
            max-width: 900px;
        }
        
        .section-divider {
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--highlight), transparent);
            margin: 4rem 0;
        }
        
        .citation {
            display: inline-block;
            background: var(--highlight);
            color: white;
            padding: 0.125rem 0.375rem;
            border-radius: 0.25rem;
            font-size: 0.75rem;
            font-weight: 600;
            text-decoration: none;
            margin-left: 0.25rem;
            transition: all 0.2s;
        }
        
        .citation:hover {
            background: #ff6b6b;
            transform: translateY(-1px);
        }
        
        /* Mermaid chart styling */
        .mermaid-container {
            display: flex;
            justify-content: center;
            min-height: 300px;
            max-height: 800px;
            background: #ffffff;
            border: 2px solid #e5e7eb;
            border-radius: 12px;
            padding: 30px;
            margin: 30px 0;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
            position: relative;
            overflow: hidden;
        }

        .mermaid-container .mermaid {
            width: 100%;
            max-width: 100%;
            height: 100%;
            cursor: grab;
            transition: transform 0.3s ease;
            transform-origin: center center;
            display: flex;
            justify-content: center;
            align-items: center;
            touch-action: none; /* 防止触摸设备上的默认行为 */
            -webkit-user-select: none; /* 防止文本选择 */
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }

        .mermaid-container .mermaid svg {
            max-width: 100%;
            height: 100%;
            display: block;
            margin: 0 auto;
        }

        .mermaid-container .mermaid:active {
            cursor: grabbing;
        }

        .mermaid-container.zoomed .mermaid {
            height: 100%;
            width: 100%;
            cursor: grab;
        }

        .mermaid-controls {
            position: absolute;
            top: 15px;
            right: 15px;
            display: flex;
            gap: 10px;
            z-index: 20;
            background: rgba(255, 255, 255, 0.95);
            padding: 8px;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        }

        .mermaid-control-btn {
            background: #ffffff;
            border: 1px solid #d1d5db;
            border-radius: 6px;
            padding: 10px;
            cursor: pointer;
            transition: all 0.2s ease;
            color: #374151;
            font-size: 14px;
            min-width: 36px;
            height: 36px;
            text-align: center;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .mermaid-control-btn:hover {
            background: #f8fafc;
            border-color: #3b82f6;
            color: #3b82f6;
            transform: translateY(-1px);
        }

        .mermaid-control-btn:active {
            transform: scale(0.95);
        }

        /* Enhanced node styling for better contrast */
        .mermaid .node rect,
        .mermaid .node circle,
        .mermaid .node ellipse,
        .mermaid .node polygon {
            stroke: var(--primary) !important;
            stroke-width: 2px !important;
            filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
        }
        
        .mermaid .node .label {
            color: var(--primary) !important;
            font-weight: 600 !important;
            font-size: 14px !important;
            font-family: 'Inter', sans-serif !important;
            text-shadow: 0 1px 2px rgba(255, 255, 255, 0.8);
        }
        
        .mermaid .edgePath .path {
            stroke: var(--accent) !important;
            stroke-width: 2px !important;
            filter: drop-shadow(0 1px 2px rgba(0, 0, 0, 0.1));
        }
        
        .mermaid .edgeLabel {
            background-color: white !important;
            color: var(--primary) !important;
            font-weight: 600 !important;
            padding: 4px 8px !important;
            border-radius: 4px !important;
            border: 1px solid var(--accent) !important;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1) !important;
        }
        
        /* Ensure text readability on all node colors */
        .mermaid .node[style*="fill:#1a1a2e"] .label,
        .mermaid .node[style*="fill:#0f3460"] .label,
        .mermaid .node[style*="fill:#16213e"] .label {
            color: white !important;
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.8) !important;
        }
        
        .mermaid .node[style*="fill:#e94560"] .label {
            color: white !important;
            text-shadow: 0 1px 2px rgba(0, 0, 0, 0.8) !important;
            font-weight: 700 !important;
        }
        
        .mermaid .node[style*="fill:#f8fafc"] .label,
        .mermaid .node[style*="fill:#ffffff"] .label {
            color: var(--primary) !important;
            text-shadow: 0 1px 2px rgba(255, 255, 255, 0.8) !important;
        }
        
        @media (max-width: 1280px) {
            .toc-fixed { display: none; }
            .content-main { margin-left: 0; max-width: 100%; }
        }

        @media (max-width: 1024px) {
            .mermaid-control-btn:not(.reset-zoom) {
                display: none;
            }
            .mermaid-controls {
                top: auto;
                bottom: 15px;
                right: 15px;
            }
        }

        @media (max-width: 768px) {
            .bento-grid {
                display: flex;
                flex-direction: column;
                height: auto;
            }
            .bento-main {
                min-height: 50vh;
            }
            .bento-main h1 {
                font-size: 2.5rem;
            }
            .bento-main p {
                font-size: 1rem;
            }
            .floating-element {
                display: none;
            }
            .content-main {
                padding: 1rem;
            }
        }

        @media (max-width: 640px) {
            .bento-main h1 {
                font-size: 2rem;
            }
            .bento-main p {
                font-size: 0.9rem;
            }
            .mermaid-container {
                padding: 15px;
            }
        }
    </style>
  </head>

  <body>
    <!-- Fixed Table of Contents -->
    <nav class="toc-fixed">
      <h3 class="font-canela font-bold text-lg text-gray-800 mb-4">Contents</h3>
      <ul class="space-y-2 text-sm">
        <li>
          <a class="block py-1 px-2 rounded hover:bg-gray-100 transition-colors" href="#overview">Project Overview</a>
        </li>
        <li>
          <a class="block py-1 px-2 rounded hover:bg-gray-100 transition-colors" href="#features">Key Features</a>
        </li>
        <li>
          <a class="block py-1 px-2 rounded hover:bg-gray-100 transition-colors" href="#architecture">Technical Architecture</a>
        </li>
        <li>
          <a class="block py-1 px-2 rounded hover:bg-gray-100 transition-colors" href="#ux">User Experience</a>
        </li>
        <li>
          <a class="block py-1 px-2 rounded hover:bg-gray-100 transition-colors" href="#curriculum">Learning Paths</a>
        </li>
        <li>
          <a class="block py-1 px-2 rounded hover:bg-gray-100 transition-colors" href="#code">Code Examples</a>
        </li>
      </ul>
    </nav>

    <!-- Main Content -->
    <div class="content-main mx-auto px-8 py-12">
      <!-- Hero Section with Bento Grid -->
      <section class="mb-20">
        <div class="bento-grid">
          <!-- Main Hero Content -->
          <div class="bento-main flex flex-col justify-center p-12 relative">
            <div class="floating-element w-32 h-32 top-10 left-10"></div>
            <div class="floating-element w-24 h-24 bottom-20 right-20" style="animation-delay: -2s;"></div>
            <div class="floating-element w-16 h-16 top-1/2 right-10" style="animation-delay: -4s;"></div>

            <div class="relative z-10">
              <h1 class="font-canela text-6xl font-bold text-white mb-6 leading-tight">
                <span class="italic">Arcium</span> Academy
              </h1>
              <p class="text-xl text-gray-200 mb-8 leading-relaxed">
                A revolutionary learning platform democratizing Web3, privacy technologies, and advanced cryptography through interactive, gamified education.
              </p>
              <div class="flex space-x-4">
                <span class="bg-white bg-opacity-20 text-white px-4 py-2 rounded-full text-sm font-medium">Interactive Learning</span>
                <span class="bg-white bg-opacity-20 text-white px-4 py-2 rounded-full text-sm font-medium">Decentralized</span>
                <span class="bg-white bg-opacity-20 text-white px-4 py-2 rounded-full text-sm font-medium">Gamified</span>
              </div>
            </div>
            <div class="absolute inset-0 opacity-20">
              <img alt="Abstract visualization of interconnected nodes representing knowledge networks" class="w-full h-full object-cover" src="https://kimi-web-img.moonshot.cn/img/www.hakia.com/00dda286f5fed710a7c3b55257621b59120ca60e" size="wallpaper" aspect="wide" query="abstract knowledge network nodes interconnected" referrerpolicy="no-referrer" data-modified="1" data-score="0.00"/>
            </div>
          </div>

          <!-- Side Panel 1 -->
          <div class="bento-side-1 p-8 flex flex-col justify-center">
            <h3 class="font-canela text-2xl font-bold text-gray-800 mb-4">Core Mission</h3>
            <p class="text-gray-600 leading-relaxed">
              Democratize access to advanced education in Web3, privacy, and cryptography through an interactive, community-driven platform that adapts to each learner&#39;s journey.
            </p>
          </div>

          <!-- Side Panel 2 -->
          <div class="bento-side-2 p-8 flex flex-col justify-center">
            <h3 class="font-canela text-2xl font-bold text-gray-800 mb-4">Ecosystem Integration</h3>
            <p class="text-gray-600 leading-relaxed">
              Deeply integrated with the Arcium ecosystem, serving as the primary educational pipeline for projects like Umbra, Darkpool, and MXES.
            </p>
          </div>
        </div>
      </section>

      <!-- Project Overview -->
      <section class="mb-20" id="overview">
        <h2 class="font-canela text-4xl font-bold mb-8">Project Overview: The ACA Arcium Academy Vision</h2>

        <div class="prose prose-lg max-w-none mb-12">
          <p class="text-gray-700 leading-relaxed mb-6">
            The ACA Arcium Academy represents a groundbreaking initiative in the field of digital education, specifically tailored to the burgeoning domains of Web3, privacy-enhancing technologies, and advanced cryptographic protocols. The project&#39;s vision is to create a comprehensive, interactive, and gamified learning ecosystem that not only imparts theoretical knowledge but also provides hands-on experience with cutting-edge technologies.
          </p>

          <p class="text-gray-700 leading-relaxed mb-6">
            The academy is designed to be an integral part of the broader ACA Arcium ecosystem, leveraging its research and development to offer a curriculum that is both current and deeply practical. By fostering a community-driven environment, the academy aims to cultivate a new generation of experts who can contribute to and advance the Arcium ecosystem and the wider Web3 landscape.
            <a class="citation" href="#ref-1">[1]</a>
          </p>
        </div>

        <!-- Architecture Diagram -->
        <div class="bg-white rounded-2xl p-8 shadow-lg mb-12">
          <h3 class="font-canela text-2xl font-bold mb-6">Platform Architecture</h3>
          <div class="mermaid-container">
            <div class="mermaid-controls">
              <button class="mermaid-control-btn zoom-in" title="放大">
                <i class="fas fa-search-plus"></i>
              </button>
              <button class="mermaid-control-btn zoom-out" title="缩小">
                <i class="fas fa-search-minus"></i>
              </button>
              <button class="mermaid-control-btn reset-zoom" title="重置">
                <i class="fas fa-expand-arrows-alt"></i>
              </button>
              <button class="mermaid-control-btn fullscreen" title="全屏查看">
                <i class="fas fa-expand"></i>
              </button>
            </div>
            <div class="mermaid">
              graph TB
              A[&#34;User Interface&#34;] --&gt; B[&#34;Adaptive Learning Engine&#34;]
              B --&gt; C[&#34;Gamification System&#34;]
              B --&gt; D[&#34;Content Management&#34;]
              C --&gt; E[&#34;Encrypted Experience Credits&#34;]
              D --&gt; F[&#34;IPFS Content Distribution&#34;]
              G[&#34;Community Platform&#34;] --&gt; H[&#34;Collaboration Tools&#34;]
              I[&#34;Blockchain Integration&#34;] --&gt; J[&#34;Secure Credentialing&#34;]
              K[&#34;Progress Tracking&#34;] --&gt; L[&#34;Personalized Dashboard&#34;]

              style A fill:#1a1a2e,stroke:#0f3460,stroke-width:2px,color:#fff
              style E fill:#e94560,stroke:#d63447,stroke-width:2px,color:#fff
              style F fill:#f8fafc,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style J fill:#16213e,stroke:#0f3460,stroke-width:2px,color:#fff
              style L fill:#e94560,stroke:#d63447,stroke-width:2px,color:#fff
              style B fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style C fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style D fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style G fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style H fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style I fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
              style K fill:#ffffff,stroke:#0f3460,stroke-width:2px,color:#1a1a2e
            </div>
          </div>
          <p class="text-sm text-gray-600 mt-4 text-center">
            <em>Interactive platform architecture showing the interconnected components of the learning ecosystem</em>
          </p>
        </div>

        <div class="grid md:grid-cols-2 gap-8 mb-12">
          <div class="bg-gradient-to-br from-blue-50 to-indigo-50 p-8 rounded-2xl">
            <h3 class="font-canela text-2xl font-bold mb-4">Core Mission</h3>
            <p class="text-gray-700 leading-relaxed">
              Democratize access to advanced education in Web3, privacy, and cryptography, making these complex subjects accessible and engaging for a global audience through interactive challenges and adaptive learning paths.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
          </div>

          <div class="bg-gradient-to-br from-rose-50 to-pink-50 p-8 rounded-2xl">
            <h3 class="font-canela text-2xl font-bold mb-4">Ecosystem Integration</h3>
            <p class="text-gray-700 leading-relaxed">
              Deeply integrated component of the larger ACA Arcium ecosystem, ensuring educational content aligns with latest developments while serving customized learning paths for projects like Umbra, Darkpool, and MXES.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
          </div>
        </div>

        <div class="bg-white p-8 rounded-2xl shadow-lg">
          <h3 class="font-canela text-2xl font-bold mb-6">Target Audience</h3>
          <div class="grid md:grid-cols-3 gap-6">
            <div class="text-center">
              <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-seedling text-2xl text-blue-600"></i>
              </div>
              <h4 class="font-bold text-lg mb-2">Beginners</h4>
              <p class="text-gray-600 text-sm">Foundational courses covering blockchain basics, smart contracts, and decentralized applications</p>
            </div>
            <div class="text-center">
              <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-tree text-2xl text-green-600"></i>
              </div>
              <h4 class="font-bold text-lg mb-2">Intermediate</h4>
              <p class="text-gray-600 text-sm">Advanced topics including MPC, C-SPL, and privacy-enhancing technologies</p>
            </div>
            <div class="text-center">
              <div class="w-16 h-16 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-mountain text-2xl text-purple-600"></i>
              </div>
              <h4 class="font-bold text-lg mb-2">Advanced</h4>
              <p class="text-gray-600 text-sm">Research track for original contributions to cryptography and Web3 technologies</p>
            </div>
          </div>
        </div>
      </section>

      <div class="section-divider"></div>

      <!-- Key Features -->
      <section class="mb-20" id="features">
        <h2 class="font-canela text-4xl font-bold mb-8">Key Features of the Interactive Learning Platform</h2>

        <div class="space-y-12">
          <!-- Gamified Learning -->
          <div class="bg-gradient-to-r from-orange-50 to-amber-50 p-8 rounded-2xl">
            <div class="flex items-start space-x-6">
              <div class="w-16 h-16 bg-orange-500 rounded-xl flex items-center justify-center flex-shrink-0">
                <i class="fas fa-gamepad text-white text-2xl"></i>
              </div>
              <div>
                <h3 class="font-canela text-2xl font-bold mb-4">Interactive and Gamified Learning Environment</h3>
                <p class="text-gray-700 leading-relaxed mb-4">
                  At the heart of the ACA Arcium Academy is a highly interactive and gamified learning environment that transforms education into an engaging adventure. The platform incorporates challenges, badges, and leaderboards to motivate users and encourage active participation.
                  <a class="citation" href="#ref-1">[1]</a>
                </p>
                <div class="grid md:grid-cols-3 gap-4">
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-orange-600 mb-2">EEC Rewards</h4>
                    <p class="text-sm text-gray-600">Encrypted Experience Credits earned through challenge completion</p>
                  </div>
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-orange-600 mb-2">Badge System</h4>
                    <p class="text-sm text-gray-600">Visual representation of skills and achievements</p>
                  </div>
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-orange-600 mb-2">Leaderboards</h4>
                    <p class="text-sm text-gray-600">Friendly competition driving engagement</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Comprehensive Curriculum -->
          <div class="bg-gradient-to-r from-blue-50 to-cyan-50 p-8 rounded-2xl">
            <div class="flex items-start space-x-6">
              <div class="w-16 h-16 bg-blue-500 rounded-xl flex items-center justify-center flex-shrink-0">
                <i class="fas fa-book-open text-white text-2xl"></i>
              </div>
              <div>
                <h3 class="font-canela text-2xl font-bold mb-4">Comprehensive Curriculum</h3>
                <p class="text-gray-700 leading-relaxed mb-4">
                  The academy offers a comprehensive and up-to-date curriculum covering the full spectrum of Web3, privacy, and advanced cryptographic technologies. The curriculum is organized into structured learning paths with a strong emphasis on real-world applications.
                  <a class="citation" href="#ref-1">[1]</a>
                </p>
                <div class="bg-white p-6 rounded-lg">
                  <h4 class="font-bold text-blue-600 mb-3">Key Technologies Covered:</h4>
                  <ul class="grid md:grid-cols-2 gap-2 text-sm text-gray-600">
                    <li>• Multiparty Computation (MPC)</li>
                    <li>• Confidential Solana Program Library (C-SPL)</li>
                    <li>• Zero-Knowledge Proofs</li>
                    <li>• Privacy-Preserving Computation</li>
                    <li>• Smart Contract Development</li>
                    <li>• Decentralized Application Architecture</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>

          <!-- Decentralized Infrastructure -->
          <div class="bg-gradient-to-r from-green-50 to-emerald-50 p-8 rounded-2xl">
            <div class="flex items-start space-x-6">
              <div class="w-16 h-16 bg-green-500 rounded-xl flex items-center justify-center flex-shrink-0">
                <i class="fas fa-shield-alt text-white text-2xl"></i>
              </div>
              <div>
                <h3 class="font-canela text-2xl font-bold mb-4">Decentralized and Secure Learning Experience</h3>
                <p class="text-gray-700 leading-relaxed mb-4">
                  Built on principles of decentralization and security, the platform leverages IPFS for content distribution, ensuring resilience and censorship-resistance while maintaining user privacy and data integrity.
                  <a class="citation" href="#ref-1">[1]</a>
                </p>
                <div class="grid md:grid-cols-2 gap-4">
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-green-600 mb-2">Security Features</h4>
                    <ul class="text-sm text-gray-600 space-y-1">
                      <li>• Encrypted user data</li>
                      <li>• Decentralized storage (IPFS)</li>
                      <li>• Rate limiting and audit logging</li>
                    </ul>
                  </div>
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-green-600 mb-2">Privacy Protection</h4>
                    <ul class="text-sm text-gray-600 space-y-1">
                      <li>• End-to-end encryption</li>
                      <li>• User-controlled permissions</li>
                      <li>• Anonymous learning paths</li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Adaptive Learning -->
          <div class="bg-gradient-to-r from-purple-50 to-violet-50 p-8 rounded-2xl">
            <div class="flex items-start space-x-6">
              <div class="w-16 h-16 bg-purple-500 rounded-xl flex items-center justify-center flex-shrink-0">
                <i class="fas fa-brain text-white text-2xl"></i>
              </div>
              <div>
                <h3 class="font-canela text-2xl font-bold mb-4">Adaptive and Personalized Learning Paths</h3>
                <p class="text-gray-700 leading-relaxed mb-4">
                  The platform&#39;s adaptive learning engine tracks user progress and performance, recommending personalized learning paths and content to ensure optimal learning pace and relevance to individual goals.
                  <a class="citation" href="#ref-1">[1]</a>
                </p>
                <div class="bg-white p-6 rounded-lg">
                  <div class="grid md:grid-cols-3 gap-4">
                    <div class="text-center">
                      <div class="w-12 h-12 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-2">
                        <i class="fas fa-chart-line text-purple-600"></i>
                      </div>
                      <h5 class="font-bold text-sm">Progress Tracking</h5>
                    </div>
                    <div class="text-center">
                      <div class="w-12 h-12 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-2">
                        <i class="fas fa-route text-purple-600"></i>
                      </div>
                      <h5 class="font-bold text-sm">Dynamic Pathing</h5>
                    </div>
                    <div class="text-center">
                      <div class="w-12 h-12 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-2">
                        <i class="fas fa-cogs text-purple-600"></i>
                      </div>
                      <h5 class="font-bold text-sm">Custom Modules</h5>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Community Features -->
          <div class="bg-gradient-to-r from-rose-50 to-pink-50 p-8 rounded-2xl">
            <div class="flex items-start space-x-6">
              <div class="w-16 h-16 bg-rose-500 rounded-xl flex items-center justify-center flex-shrink-0">
                <i class="fas fa-users text-white text-2xl"></i>
              </div>
              <div>
                <h3 class="font-canela text-2xl font-bold mb-4">Community-Driven Content and Collaboration</h3>
                <p class="text-gray-700 leading-relaxed mb-4">
                  More than just a learning platform, the academy fosters a vibrant community of learners, educators, and experts. Features include discussion forums, real-time collaboration tools, and mentorship programs.
                  <a class="citation" href="#ref-1">[1]</a>
                </p>
                <div class="grid md:grid-cols-2 gap-4">
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-rose-600 mb-2">Collaboration Tools</h4>
                    <ul class="text-sm text-gray-600 space-y-1">
                      <li>• Shared workspaces</li>
                      <li>• Real-time chat</li>
                      <li>• Video conferencing</li>
                    </ul>
                  </div>
                  <div class="bg-white p-4 rounded-lg">
                    <h4 class="font-bold text-rose-600 mb-2">Community Programs</h4>
                    <ul class="text-sm text-gray-600 space-y-1">
                      <li>• Expert mentorship</li>
                      <li>• Peer-to-peer learning</li>
                      <li>• Collaborative projects</li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <div class="section-divider"></div>

      <!-- Technical Architecture -->
      <section class="mb-20" id="architecture">
        <h2 class="font-canela text-4xl font-bold mb-8">Technical Architecture and System Design</h2>

        <div class="bg-white p-8 rounded-2xl shadow-lg mb-12">
          <p class="text-gray-700 leading-relaxed mb-8">
            The technical architecture of the ACA Arcium Academy is designed to be scalable, robust, and secure, providing a solid foundation for the platform&#39;s innovative learning features. The architecture is based on a modern microservices approach, allowing for high flexibility and scalability.
            <a class="citation" href="#ref-1">[1]</a>
          </p>

          <!-- Technology Stack Diagram -->
          <div class="mb-8">
            <h3 class="font-canela text-2xl font-bold mb-6 text-center">Technology Stack Overview</h3>
            <div class="mermaid-container">
              <div class="mermaid-controls">
                <button class="mermaid-control-btn zoom-in" title="放大">
                  <i class="fas fa-search-plus"></i>
                </button>
                <button class="mermaid-control-btn zoom-out" title="缩小">
                  <i class="fas fa-search-minus"></i>
                </button>
                <button class="mermaid-control-btn reset-zoom" title="重置">
                  <i class="fas fa-expand-arrows-alt"></i>
                </button>
                <button class="mermaid-control-btn fullscreen" title="全屏查看">
                  <i class="fas fa-expand"></i>
                </button>
              </div>
              <div class="mermaid">
                graph TD
                FE[&#34;Frontend
                <br/>React.js&#34;] --&gt; BE[&#34;Backend
                <br/>Node.js + Express&#34;]
                BE --&gt; DB[&#34;Database
                <br/>MongoDB&#34;]
                BE --&gt; IPFS[&#34;Content Distribution
                <br/>IPFS&#34;]
                BE --&gt; ETH[&#34;Blockchain Integration
                <br/>Ethereum&#34;]
                FE --&gt; UI[&#34;User Interface
                <br/>Interactive Components&#34;]

                style FE fill:#61dafb,stroke:#282c34,stroke-width:2px,color:#fff
                style BE fill:#68a063,stroke:#3c873a,stroke-width:2px,color:#fff
                style DB fill:#4db33d,stroke:#3c873a,stroke-width:2px,color:#fff
                style IPFS fill:#65c2cb,stroke:#4a9d9b,stroke-width:2px,color:#fff
                style ETH fill:#627eea,stroke:#3c3c3d,stroke-width:2px,color:#fff
                style UI fill:#ff6b6b,stroke:#d63447,stroke-width:2px,color:#fff
              </div>
            </div>
            <p class="text-sm text-gray-600 mt-4 text-center">
              <em>Complete technology stack showing frontend, backend, database, and decentralized storage integration</em>
            </p>
          </div>

          <div class="grid md:grid-cols-2 gap-8">
            <!-- Frontend -->
            <div class="bg-blue-50 p-6 rounded-xl">
              <div class="flex items-center mb-4">
                <div class="w-12 h-12 bg-blue-500 rounded-lg flex items-center justify-center mr-4">
                  <i class="fab fa-react text-white text-xl"></i>
                </div>
                <h3 class="font-canela text-xl font-bold">Frontend</h3>
              </div>
              <h4 class="font-bold text-blue-600 mb-2">React.js</h4>
              <p class="text-gray-700 text-sm leading-relaxed">
                Component-based architecture with virtual DOM for efficient, responsive user interfaces. Enables modular UI components and optimal performance for interactive learning experiences.
                <a class="citation" href="#ref-1">[1]</a>
              </p>
            </div>

            <!-- Backend -->
            <div class="bg-green-50 p-6 rounded-xl">
              <div class="flex items-center mb-4">
                <div class="w-12 h-12 bg-green-500 rounded-lg flex items-center justify-center mr-4">
                  <i class="fab fa-node-js text-white text-xl"></i>
                </div>
                <h3 class="font-canela text-xl font-bold">Backend</h3>
              </div>
              <h4 class="font-bold text-green-600 mb-2">Node.js + Express</h4>
              <p class="text-gray-700 text-sm leading-relaxed">
                Non-blocking, event-driven architecture for scalable API services. Express provides a minimalist framework for building robust web applications and APIs.
                <a class="citation" href="#ref-1">[1]</a>
              </p>
            </div>

            <!-- Database -->
            <div class="bg-purple-50 p-6 rounded-xl">
              <div class="flex items-center mb-4">
                <div class="w-12 h-12 bg-purple-500 rounded-lg flex items-center justify-center mr-4">
                  <i class="fas fa-database text-white text-xl"></i>
                </div>
                <h3 class="font-canela text-xl font-bold">Data Management</h3>
              </div>
              <h4 class="font-bold text-purple-600 mb-2">MongoDB</h4>
              <p class="text-gray-700 text-sm leading-relaxed">
                Document-oriented NoSQL database for flexible, scalable user data and progress tracking. JSON-like storage format accommodates unstructured data.
                <a class="citation" href="#ref-1">[1]</a>
              </p>
            </div>

            <!-- Decentralized Infrastructure -->
            <div class="bg-teal-50 p-6 rounded-xl">
              <div class="flex items-center mb-4">
                <div class="w-12 h-12 bg-teal-500 rounded-lg flex items-center justify-center mr-4">
                  <i class="fas fa-network-wired text-white text-xl"></i>
                </div>
                <h3 class="font-canela text-xl font-bold">Decentralized Infrastructure</h3>
              </div>
              <h4 class="font-bold text-teal-600 mb-2">IPFS</h4>
              <p class="text-gray-700 text-sm leading-relaxed">
                InterPlanetary File System for decentralized content distribution. Peer-to-peer network ensures resilience, censorship-resistance, and content authenticity through content-addressing.
                <a class="citation" href="#ref-1">[1]</a>
              </p>
            </div>
          </div>

          <!-- Blockchain Integration -->
          <div class="mt-8 bg-yellow-50 p-6 rounded-xl">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-yellow-500 rounded-lg flex items-center justify-center mr-4">
                <i class="fab fa-ethereum text-white text-xl"></i>
              </div>
              <h3 class="font-canela text-xl font-bold">Blockchain Integration</h3>
            </div>
            <h4 class="font-bold text-yellow-600 mb-2">Ethereum for Secure Credentialing</h4>
            <p class="text-gray-700 text-sm leading-relaxed">
              Integration with Ethereum blockchain provides immutable, transparent credentialing system. Credentials issued on-chain cannot be altered or deleted, ensuring authenticity and trustworthiness.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
          </div>
        </div>
      </section>

      <div class="section-divider"></div>

      <!-- User Experience -->
      <section class="mb-20" id="ux">
        <h2 class="font-canela text-4xl font-bold mb-8">User Experience and Interface Design</h2>

        <div class="grid md:grid-cols-2 gap-8 mb-12">
          <div class="bg-white p-8 rounded-2xl shadow-lg">
            <h3 class="font-canela text-2xl font-bold mb-4">Modern, Personalized Dashboard</h3>
            <p class="text-gray-700 leading-relaxed mb-6">
              The central hub for the user&#39;s learning journey, featuring dynamic layouts that adapt to individual needs. Interactive widgets provide real-time feedback on progress and achievements.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
            <div class="space-y-3">
              <div class="flex items-center space-x-3">
                <div class="w-3 h-3 bg-blue-500 rounded-full"></div>
                <span class="text-sm text-gray-600">Progress tracking and analytics</span>
              </div>
              <div class="flex items-center space-x-3">
                <div class="w-3 h-3 bg-green-500 rounded-full"></div>
                <span class="text-sm text-gray-600">Personalized news feed</span>
              </div>
              <div class="flex items-center space-x-3">
                <div class="w-3 h-3 bg-purple-500 rounded-full"></div>
                <span class="text-sm text-gray-600">Customizable widget layout</span>
              </div>
            </div>
          </div>

          <div class="bg-white p-8 rounded-2xl shadow-lg">
            <h3 class="font-canela text-2xl font-bold mb-4">Interactive Learning Modules</h3>
            <p class="text-gray-700 leading-relaxed mb-6">
              Curriculum delivered through hands-on modules featuring quizzes, coding exercises, and real-world simulations. Built around &#34;learning by doing&#34; philosophy with immediate feedback.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
            <div class="space-y-3">
              <div class="flex items-center space-x-3">
                <div class="w-3 h-3 bg-orange-500 rounded-full"></div>
                <span class="text-sm text-gray-600">Drag-and-drop interfaces</span>
              </div>
              <div class="flex items-center space-x-3">
                <div class="w-3 h-3 bg-rose-500 rounded-full"></div>
                <span class="text-sm text-gray-600">Interactive visualizations</span>
              </div>
              <div class="flex items-center space-x-3">
                <div class="w-3 h-3 bg-teal-500 rounded-full"></div>
                <span class="text-sm text-gray-600">Real-time code execution</span>
              </div>
            </div>
          </div>
        </div>

        <div class="bg-gradient-to-r from-gray-50 to-slate-50 p-8 rounded-2xl">
          <h3 class="font-canela text-2xl font-bold mb-6">Cross-Platform Accessibility</h3>
          <div class="grid md:grid-cols-3 gap-6">
            <div class="text-center">
              <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-desktop text-2xl text-blue-600"></i>
              </div>
              <h4 class="font-bold mb-2">Desktop</h4>
              <p class="text-sm text-gray-600">Full-featured experience optimized for larger screens</p>
            </div>
            <div class="text-center">
              <div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-tablet-alt text-2xl text-green-600"></i>
              </div>
              <h4 class="font-bold mb-2">Tablet</h4>
              <p class="text-sm text-gray-600">Responsive design adapting to touch interfaces</p>
            </div>
            <div class="text-center">
              <div class="w-16 h-16 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-4">
                <i class="fas fa-mobile-alt text-2xl text-purple-600"></i>
              </div>
              <h4 class="font-bold mb-2">Mobile</h4>
              <p class="text-sm text-gray-600">On-the-go learning with full functionality</p>
            </div>
          </div>
          <p class="text-gray-700 mt-6 text-center">
            Responsive design ensures consistent experience across all devices, making education accessible to a global audience.
            <a class="citation" href="#ref-1">[1]</a>
          </p>
        </div>
      </section>

      <div class="section-divider"></div>

      <!-- Learning Paths -->
      <section class="mb-20" id="curriculum">
        <h2 class="font-canela text-4xl font-bold mb-8">Structured Learning Paths and Curriculum</h2>

        <p class="text-gray-700 leading-relaxed mb-12">
          The ACA Arcium Academy offers structured and comprehensive curriculum organized into clear learning paths, each designed to cater to specific areas of interest or expertise levels. The paths provide both broad foundations and deep, specialized knowledge.
          <a class="citation" href="#ref-1">[1]</a>
        </p>

        <!-- Learning Paths Table -->
        <div class="bg-white rounded-2xl shadow-lg overflow-hidden mb-12">
          <div class="overflow-x-auto">
            <table class="w-full">
              <thead class="bg-gray-50">
                <tr>
                  <th class="px-6 py-4 text-left text-sm font-bold text-gray-900">Learning Path</th>
                  <th class="px-6 py-4 text-left text-sm font-bold text-gray-900">Target Audience</th>
                  <th class="px-6 py-4 text-left text-sm font-bold text-gray-900">Key Topics</th>
                  <th class="px-6 py-4 text-left text-sm font-bold text-gray-900">Learning Objectives</th>
                </tr>
              </thead>
              <tbody class="divide-y divide-gray-200">
                <tr class="hover:bg-gray-50">
                  <td class="px-6 py-4">
                    <div class="flex items-center">
                      <div class="w-3 h-3 bg-blue-500 rounded-full mr-3"></div>
                      <span class="font-bold text-blue-600">Introduction to Web3</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 text-sm text-gray-700">Beginners</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Blockchain, Smart Contracts, dApps</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Build foundational understanding of decentralized technologies and develop basic dApp development skills.</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="px-6 py-4">
                    <div class="flex items-center">
                      <div class="w-3 h-3 bg-green-500 rounded-full mr-3"></div>
                      <span class="font-bold text-green-600">Advanced Cryptography</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 text-sm text-gray-700">Intermediate/Advanced</td>
                  <td class="px-6 py-4 text-sm text-gray-700">MPC, C-SPL, Zero-Knowledge Proofs</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Gain deep theoretical and practical knowledge of advanced cryptographic protocols for privacy and security.</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="px-6 py-4">
                    <div class="flex items-center">
                      <div class="w-3 h-3 bg-purple-500 rounded-full mr-3"></div>
                      <span class="font-bold text-purple-600">Privacy Technologies</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 text-sm text-gray-700">Intermediate/Advanced</td>
                  <td class="px-6 py-4 text-sm text-gray-700">ZKPs, Homomorphic Encryption, Differential Privacy</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Master the tools and techniques for designing and building privacy-preserving applications.</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="px-6 py-4">
                    <div class="flex items-center">
                      <div class="w-3 h-3 bg-orange-500 rounded-full mr-3"></div>
                      <span class="font-bold text-orange-600">Development Bootcamp</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 text-sm text-gray-700">Intermediate/Advanced</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Full-Stack dApp Development, DeFi, DAOs</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Acquire hands-on experience in building, testing, and deploying sophisticated decentralized applications.</td>
                </tr>
                <tr class="hover:bg-gray-50">
                  <td class="px-6 py-4">
                    <div class="flex items-center">
                      <div class="w-3 h-3 bg-red-500 rounded-full mr-3"></div>
                      <span class="font-bold text-red-600">Research Track</span>
                    </div>
                  </td>
                  <td class="px-6 py-4 text-sm text-gray-700">Advanced Contributors</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Original Research, Formal Verification</td>
                  <td class="px-6 py-4 text-sm text-gray-700">Contribute to the academic and open-source communities through original research in cryptography and Web3.</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>

        <!-- Learning Path Flow -->
        <div class="bg-white p-8 rounded-2xl shadow-lg">
          <h3 class="font-canela text-2xl font-bold mb-6 text-center">Learning Path Progression</h3>
          <div class="mermaid-container">
            <div class="mermaid-controls">
              <button class="mermaid-control-btn zoom-in" title="放大">
                <i class="fas fa-search-plus"></i>
              </button>
              <button class="mermaid-control-btn zoom-out" title="缩小">
                <i class="fas fa-search-minus"></i>
              </button>
              <button class="mermaid-control-btn reset-zoom" title="重置">
                <i class="fas fa-expand-arrows-alt"></i>
              </button>
              <button class="mermaid-control-btn fullscreen" title="全屏查看">
                <i class="fas fa-expand"></i>
              </button>
            </div>
            <div class="mermaid">
              flowchart TD
              A[&#34;New Learner&#34;] --&gt; B{&#34;Skill Assessment&#34;}
              B --&gt;|Beginner| C[&#34;Introduction to Web3&#34;]
              B --&gt;|Intermediate| D[&#34;Advanced Cryptography&#34;]
              B --&gt;|Advanced| E[&#34;Research Track&#34;]

              C --&gt; F{&#34;Progress Evaluation&#34;}
              D --&gt; F
              F --&gt;|Continue| G[&#34;Privacy Technologies&#34;]
              F --&gt;|Specialize| H[&#34;Development Bootcamp&#34;]
              G --&gt; I[&#34;Expert Level&#34;]
              H --&gt; I
              E --&gt; I

              I --&gt; J[&#34;Community Contribution&#34;]

              style A fill:#f8fafc,stroke:#1a1a2e,stroke-width:2px,color:#1a1a2e
              style B fill:#e94560,stroke:#d63447,stroke-width:2px,color:#fff
              style C fill:#1a1a2e,stroke:#0f3460,stroke-width:2px,color:#fff
              style D fill:#16213e,stroke:#0f3460,stroke-width:2px,color:#fff
              style E fill:#0f3460,stroke:#0a2540,stroke-width:2px,color:#fff
              style F fill:#e94560,stroke:#d63447,stroke-width:2px,color:#fff
              style G fill:#1a1a2e,stroke:#0f3460,stroke-width:2px,color:#fff
              style H fill:#16213e,stroke:#0f3460,stroke-width:2px,color:#fff
              style I fill:#e94560,stroke:#d63447,stroke-width:2px,color:#fff
              style J fill:#f8fafc,stroke:#1a1a2e,stroke-width:2px,color:#1a1a2e
            </div>
          </div>
          <p class="text-sm text-gray-600 mt-4 text-center">
            <em>Adaptive learning progression showing skill assessment, path specialization, and community contribution</em>
          </p>
        </div>
      </section>

      <div class="section-divider"></div>

      <!-- Code Examples -->
      <section class="mb-20" id="code">
        <h2 class="font-canela text-4xl font-bold mb-8">Code Examples and Practical Applications</h2>

        <p class="text-gray-700 leading-relaxed mb-12">
          The ACA Arcium Academy provides learners with practical code examples and hands-on applications to ensure deep understanding of complex concepts. These examples are well-documented and designed to be easily followed and modified.
          <a class="citation" href="#ref-1">[1]</a>
        </p>

        <div class="grid md:grid-cols-2 gap-8">
          <!-- MPCT Protocol Example -->
          <div class="bg-gray-900 p-6 rounded-2xl text-white">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-blue-600 rounded-lg flex items-center justify-center mr-4">
                <i class="fas fa-lock text-white text-xl"></i>
              </div>
              <h3 class="font-canela text-xl font-bold">MPCT Protocol Implementation</h3>
            </div>
            <pre class="text-sm overflow-x-auto"><code class="language-javascript">// MPCT protocol implementation example
const mpct = require(&#39;mpct-js&#39;);

// Initialize parties
const party1 = new mpct.Party(1, 2); // Party 1 of 2
const party2 = new mpct.Party(2, 2); // Party 2 of 2

// Private inputs
const input1 = 10; // Party 1&#39;s private input
const input2 = 20; // Party 2&#39;s private input

// Perform secure computation
async function secureAddition() {
  // Party 1 shares its input
  const share1 = await party1.share(input1);
  
  // Party 2 shares its input
  const share2 = await party2.share(input2);
  
  // Both parties compute the sum
  const resultShare1 = await party1.add(share1, share2);
  const resultShare2 = await party2.add(share1, share2);
  
  // Reconstruct the result
  const result = await mpct.reconstruct(
    resultShare1, resultShare2
  );
  
  console.log(`Secure computation result: ${result}`);
  // Output: 30 (without revealing inputs)
}

secureAddition();</code></pre>
            <p class="text-gray-400 text-xs mt-4">
              Demonstrates secure multi-party computation for adding private inputs without revealing them.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
          </div>

          <!-- C-SPL Library Example -->
          <div class="bg-gray-900 p-6 rounded-2xl text-white">
            <div class="flex items-center mb-4">
              <div class="w-12 h-12 bg-green-600 rounded-lg flex items-center justify-center mr-4">
                <i class="fas fa-shield-alt text-white text-xl"></i>
              </div>
              <h3 class="font-canela text-xl font-bold">C-SPL Library Usage</h3>
            </div>
            <pre class="text-sm overflow-x-auto"><code class="language-javascript">// C-SPL library usage example
const cspl = require(&#39;cspl-lib&#39;);

// Initialize parties
const alice = new cspl.Party(&#39;Alice&#39;);
const bob = new cspl.Party(&#39;Bob&#39;);

// Establish confidential channel
async function secureCommunication() {
  // Alice initiates channel
  const channel = await alice.createChannel(
    &#39;Bob&#39;, { confidential: true }
  );
  
  // Alice sends encrypted message
  const message = &#34;Hello, Bob! This is confidential.&#34;;
  const encrypted = await channel.encrypt(message);
  
  // Bob receives and decrypts
  const decrypted = await bob.decrypt(
    encrypted, &#39;Alice&#39;
  );
  
  console.log(`Decrypted message: ${decrypted}`);
  
  // Verify channel security
  console.log(`Channel secure: ${channel.isSecure()}`);
}

secureCommunication();</code></pre>
            <p class="text-gray-400 text-xs mt-4">
              Shows how to establish confidential communication channels using C-SPL library.
              <a class="citation" href="#ref-1">[1]</a>
            </p>
          </div>
        </div>

        <!-- Practical Applications -->
        <div class="mt-12 bg-gradient-to-r from-indigo-50 to-blue-50 p-8 rounded-2xl">
          <h3 class="font-canela text-2xl font-bold mb-6">Practical Application Scenarios</h3>
          <div class="grid md:grid-cols-3 gap-6">
            <div class="bg-white p-6 rounded-xl">
              <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center mb-4">
                <i class="fas fa-vote-yea text-blue-600 text-xl"></i>
              </div>
              <h4 class="font-bold mb-2">Secure Voting System</h4>
              <p class="text-sm text-gray-600">Implement MPC-based voting where results are calculated without revealing individual votes</p>
            </div>
            <div class="bg-white p-6 rounded-xl">
              <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center mb-4">
                <i class="fas fa-handshake text-green-600 text-xl"></i>
              </div>
              <h4 class="font-bold mb-2">Private Auctions</h4>
              <p class="text-sm text-gray-600">Create sealed-bid auctions using zero-knowledge proofs to verify bids without revealing amounts</p>
            </div>
            <div class="bg-white p-6 rounded-xl">
              <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center mb-4">
                <i class="fas fa-exchange-alt text-purple-600 text-xl"></i>
              </div>
              <h4 class="font-bold mb-2">Confidential Transactions</h4>
              <p class="text-sm text-gray-600">Build privacy-preserving payment systems using homomorphic encryption</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Conclusion -->
      <section class="mb-20">
        <div class="bg-gradient-to-r from-gray-900 to-gray-800 text-white p-12 rounded-2xl">
          <h2 class="font-canela text-4xl font-bold mb-6">The Future of Web3 Education</h2>
          <p class="text-xl leading-relaxed mb-8 text-gray-200">
            The ACA Arcium Academy represents a paradigm shift in technical education, combining cutting-edge technology with proven pedagogical approaches to democratize access to advanced cryptographic and Web3 knowledge. By fostering a community-driven, interactive, and secure learning environment, the academy is positioned to become the premier educational platform for the next generation of Web3 innovators.
          </p>
          <div class="flex flex-wrap gap-4">
            <span class="bg-white bg-opacity-20 px-4 py-2 rounded-full text-sm font-medium">Interactive Learning</span>
            <span class="bg-white bg-opacity-20 px-4 py-2 rounded-full text-sm font-medium">Decentralized Infrastructure</span>
            <span class="bg-white bg-opacity-20 px-4 py-2 rounded-full text-sm font-medium">Community-Driven</span>
            <span class="bg-white bg-opacity-20 px-4 py-2 rounded-full text-sm font-medium">Privacy-First</span>
            <span class="bg-white bg-opacity-20 px-4 py-2 rounded-full text-sm font-medium">Gamified Experience</span>
          </div>
        </div>
      </section>

      <!-- References -->
      <section>
        <h2 class="font-canela text-3xl font-bold mb-8">References</h2>
        <div class="bg-gray-50 p-6 rounded-xl">
          <p class="text-sm text-gray-700 mb-2">
            <span class="font-bold" id="ref-1">[1]</span> ACA Arcium Academy Project Documentation.
            <a class="text-blue-600 hover:underline" href="https://arcium.com/academy" target="_blank">
              https://arcium.com/academy
            </a>
          </p>
        </div>
      </section>
    </div>

    <script>
        // Initialize Mermaid with enhanced configuration
        mermaid.initialize({
            startOnLoad: true,
            theme: 'base',
            themeVariables: {
                // Primary colors with high contrast
                primaryColor: '#ffffff',
                primaryTextColor: '#1a1a2e',
                primaryBorderColor: '#0f3460',
                lineColor: '#0f3460',
                
                // Secondary colors
                secondaryColor: '#f8fafc',
                tertiaryColor: '#e94560',
                
                // Background colors
                background: '#ffffff',
                mainBkg: '#ffffff',
                secondBkg: '#f8fafc',
                tertiaryBkg: '#e94560',
                
                // Node-specific colors for better contrast
                cScale0: '#1a1a2e',  // Dark blue for headers
                cScale1: '#e94560',  // Red for highlights
                cScale2: '#f8fafc',  // Light gray for backgrounds
                cScale3: '#16213e',  // Medium blue
                cScale4: '#0f3460',  // Dark blue
                cScale5: '#ffffff',  // White
                
                // Text colors for different backgrounds
                darkTextColor: '#ffffff',
                lightTextColor: '#1a1a2e',
                
                // Edge and label styling
                edgeLabelBackground: '#ffffff',
                edgeLabelText: '#1a1a2e',
                
                // Cluster styling
                clusterBkg: '#f8fafc',
                clusterBorder: '#0f3460'
            },
            flowchart: {
                useMaxWidth: false,
                htmlLabels: true,
                curve: 'basis',
                padding: 20
            },
            graph: {
                useMaxWidth: false,
                htmlLabels: true
            },
            sequence: {
                useMaxWidth: false,
                wrap: true,
                width: 150
            },
            gantt: {
                useMaxWidth: false
            },
            // Ensure proper sizing
            maxTextSize: 90000,
            maxEdges: 200
        });

        // Initialize Mermaid Controls for zoom and pan
        function initializeMermaidControls() {
            const containers = document.querySelectorAll('.mermaid-container');

            containers.forEach(container => {
            const mermaidElement = container.querySelector('.mermaid');
            let scale = 1;
            let isDragging = false;
            let startX, startY, translateX = 0, translateY = 0;

            // 触摸相关状态
            let isTouch = false;
            let touchStartTime = 0;
            let initialDistance = 0;
            let initialScale = 1;
            let isPinching = false;

            // Zoom controls
            const zoomInBtn = container.querySelector('.zoom-in');
            const zoomOutBtn = container.querySelector('.zoom-out');
            const resetBtn = container.querySelector('.reset-zoom');
            const fullscreenBtn = container.querySelector('.fullscreen');

            function updateTransform() {
                mermaidElement.style.transform = `translate(${translateX}px, ${translateY}px) scale(${scale})`;

                if (scale > 1) {
                container.classList.add('zoomed');
                } else {
                container.classList.remove('zoomed');
                }

                mermaidElement.style.cursor = isDragging ? 'grabbing' : 'grab';
            }

            if (zoomInBtn) {
                zoomInBtn.addEventListener('click', () => {
                scale = Math.min(scale * 1.25, 4);
                updateTransform();
                });
            }

            if (zoomOutBtn) {
                zoomOutBtn.addEventListener('click', () => {
                scale = Math.max(scale / 1.25, 0.3);
                if (scale <= 1) {
                    translateX = 0;
                    translateY = 0;
                }
                updateTransform();
                });
            }

            if (resetBtn) {
                resetBtn.addEventListener('click', () => {
                scale = 1;
                translateX = 0;
                translateY = 0;
                updateTransform();
                });
            }

            if (fullscreenBtn) {
                fullscreenBtn.addEventListener('click', () => {
                if (container.requestFullscreen) {
                    container.requestFullscreen();
                } else if (container.webkitRequestFullscreen) {
                    container.webkitRequestFullscreen();
                } else if (container.msRequestFullscreen) {
                    container.msRequestFullscreen();
                }
                });
            }

            // Mouse Events
            mermaidElement.addEventListener('mousedown', (e) => {
                if (isTouch) return; // 如果是触摸设备，忽略鼠标事件

                isDragging = true;
                startX = e.clientX - translateX;
                startY = e.clientY - translateY;
                mermaidElement.style.cursor = 'grabbing';
                updateTransform();
                e.preventDefault();
            });

            document.addEventListener('mousemove', (e) => {
                if (isDragging && !isTouch) {
                translateX = e.clientX - startX;
                translateY = e.clientY - startY;
                updateTransform();
                }
            });

            document.addEventListener('mouseup', () => {
                if (isDragging && !isTouch) {
                isDragging = false;
                mermaidElement.style.cursor = 'grab';
                updateTransform();
                }
            });

            document.addEventListener('mouseleave', () => {
                if (isDragging && !isTouch) {
                isDragging = false;
                mermaidElement.style.cursor = 'grab';
                updateTransform();
                }
            });

            // 获取两点之间的距离
            function getTouchDistance(touch1, touch2) {
                return Math.hypot(
                touch2.clientX - touch1.clientX,
                touch2.clientY - touch1.clientY
                );
            }

            // Touch Events - 触摸事件处理
            mermaidElement.addEventListener('touchstart', (e) => {
                isTouch = true;
                touchStartTime = Date.now();

                if (e.touches.length === 1) {
                // 单指拖动
                isPinching = false;
                isDragging = true;

                const touch = e.touches[0];
                startX = touch.clientX - translateX;
                startY = touch.clientY - translateY;

                } else if (e.touches.length === 2) {
                // 双指缩放
                isPinching = true;
                isDragging = false;

                const touch1 = e.touches[0];
                const touch2 = e.touches[1];
                initialDistance = getTouchDistance(touch1, touch2);
                initialScale = scale;
                }

                e.preventDefault();
            }, { passive: false });

            mermaidElement.addEventListener('touchmove', (e) => {
                if (e.touches.length === 1 && isDragging && !isPinching) {
                // 单指拖动
                const touch = e.touches[0];
                translateX = touch.clientX - startX;
                translateY = touch.clientY - startY;
                updateTransform();

                } else if (e.touches.length === 2 && isPinching) {
                // 双指缩放
                const touch1 = e.touches[0];
                const touch2 = e.touches[1];
                const currentDistance = getTouchDistance(touch1, touch2);

                if (initialDistance > 0) {
                    const newScale = Math.min(Math.max(
                    initialScale * (currentDistance / initialDistance),
                    0.3
                    ), 4);
                    scale = newScale;
                    updateTransform();
                }
                }

                e.preventDefault();
            }, { passive: false });

            mermaidElement.addEventListener('touchend', (e) => {
                // 重置状态
                if (e.touches.length === 0) {
                isDragging = false;
                isPinching = false;
                initialDistance = 0;

                // 延迟重置isTouch，避免鼠标事件立即触发
                setTimeout(() => {
                    isTouch = false;
                }, 100);
                } else if (e.touches.length === 1 && isPinching) {
                // 从双指变为单指，切换为拖动模式
                isPinching = false;
                isDragging = true;

                const touch = e.touches[0];
                startX = touch.clientX - translateX;
                startY = touch.clientY - translateY;
                }

                updateTransform();
            });

            mermaidElement.addEventListener('touchcancel', (e) => {
                isDragging = false;
                isPinching = false;
                initialDistance = 0;

                setTimeout(() => {
                isTouch = false;
                }, 100);

                updateTransform();
            });

            // Enhanced wheel zoom with better center point handling
            container.addEventListener('wheel', (e) => {
                e.preventDefault();
                const rect = container.getBoundingClientRect();
                const centerX = rect.width / 2;
                const centerY = rect.height / 2;

                const delta = e.deltaY > 0 ? 0.9 : 1.1;
                const newScale = Math.min(Math.max(scale * delta, 0.3), 4);

                // Adjust translation to zoom towards center
                if (newScale !== scale) {
                const scaleDiff = newScale / scale;
                translateX = translateX * scaleDiff;
                translateY = translateY * scaleDiff;
                scale = newScale;

                if (scale <= 1) {
                    translateX = 0;
                    translateY = 0;
                }

                updateTransform();
                }
            });

            // Initialize display
            updateTransform();
            });
        }

        // Initialize the mermaid controls when the page loads
        document.addEventListener('DOMContentLoaded', function() {
            initializeMermaidControls();
        });

        // Smooth scrolling for anchor links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // Highlight active section in TOC
        const sections = document.querySelectorAll('section[id]');
        const tocLinks = document.querySelectorAll('.toc-fixed a');

        function updateActiveTocLink() {
            let current = '';
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                const sectionHeight = section.clientHeight;
                if (pageYOffset >= sectionTop - 200) {
                    current = section.getAttribute('id');
                }
            });

            tocLinks.forEach(link => {
                link.classList.remove('bg-blue-100', 'text-blue-700', 'font-medium');
                if (link.getAttribute('href') === `#${current}`) {
                    link.classList.add('bg-blue-100', 'text-blue-700', 'font-medium');
                }
            });
        }

        window.addEventListener('scroll', updateActiveTocLink);
        updateActiveTocLink(); // Initialize on load
    </script>

  

</body></html>
