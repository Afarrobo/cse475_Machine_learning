<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Disaster Response Object Detection - README</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 60px 40px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 0%, transparent 70%);
            animation: pulse 15s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.3em;
            opacity: 0.95;
            position: relative;
            z-index: 1;
        }

        .badges {
            margin-top: 20px;
            position: relative;
            z-index: 1;
        }

        .badge {
            display: inline-block;
            padding: 8px 16px;
            margin: 5px;
            background: rgba(255,255,255,0.2);
            border-radius: 20px;
            backdrop-filter: blur(10px);
            font-size: 0.9em;
            transition: transform 0.3s;
        }

        .badge:hover {
            transform: translateY(-2px);
            background: rgba(255,255,255,0.3);
        }

        .content {
            padding: 40px;
        }

        .section {
            margin-bottom: 40px;
            animation: fadeInUp 0.6s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .section-title {
            font-size: 2em;
            color: #667eea;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #667eea;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .icon {
            font-size: 1.2em;
        }

        .card {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            transition: all 0.3s;
            border-left: 5px solid #667eea;
        }

        .card:hover {
            transform: translateX(10px);
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
        }

        .card h3 {
            color: #764ba2;
            margin-bottom: 10px;
            font-size: 1.4em;
        }

        .kaggle-link {
            display: inline-block;
            background: #20beff;
            color: white;
            padding: 10px 20px;
            border-radius: 8px;
            text-decoration: none;
            margin-top: 10px;
            transition: all 0.3s;
            font-weight: 600;
        }

        .kaggle-link:hover {
            background: #1a9dd6;
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(32, 190, 255, 0.4);
        }

        .model-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .model-card {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: all 0.3s;
            border-top: 4px solid #667eea;
        }

        .model-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(102, 126, 234, 0.3);
        }

        .model-card h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.5em;
        }

        .tag {
            display: inline-block;
            background: #764ba2;
            color: white;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.85em;
            margin: 5px 5px 5px 0;
        }

        .timeline {
            position: relative;
            padding-left: 40px;
        }

        .timeline::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 3px;
            background: linear-gradient(to bottom, #667eea, #764ba2);
        }

        .timeline-item {
            position: relative;
            margin-bottom: 30px;
        }

        .timeline-item::before {
            content: '●';
            position: absolute;
            left: -47px;
            color: #667eea;
            font-size: 2em;
            line-height: 1;
        }

        .info-box {
            background: #f8f9fa;
            border-left: 4px solid #28a745;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
        }

        .info-box h4 {
            color: #28a745;
            margin-bottom: 10px;
        }

        .footer {
            background: #2d3748;
            color: white;
            padding: 40px;
            text-align: center;
        }

        .footer-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }

        .footer h3 {
            color: #667eea;
            margin-bottom: 15px;
        }

        .footer p {
            line-height: 1.8;
        }

        .highlight {
            background: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
            padding: 2px 6px;
            border-radius: 4px;
            font-weight: 600;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2em;
            }

            .content {
                padding: 20px;
            }

            .model-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>

</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🚨 Disaster Response Object Detection</h1>
            <p>Advanced YOLO-Based Detection System for Emergency Response</p>
            <div class="badges">
                <span class="badge">🔥 YOLOv10</span>
                <span class="badge">⚡ YOLOv11</span>
                <span class="badge">🚀 YOLOv12</span>
                <span class="badge">🎓 Semi-Supervised</span>
                <span class="badge">🤖 Self-Supervised</span>
            </div>
        </div>

        <div class="content">
            <!-- Project Overview -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">📖</span>
                    Project Overview
                </h2>
                <p style="font-size: 1.1em; line-height: 1.8; color: #555;">
                    This project implements state-of-the-art object detection models for disaster response scenarios.
                    By leveraging <span class="highlight">supervised</span>, <span class="highlight">semi-supervised</span>,
                    and <span class="highlight">self-supervised</span> learning approaches with the latest YOLO architectures,
                    aimed to improve emergency response efficiency through automated object detection in disaster-affected areas.
                </p>
            </div>

            <!-- Dataset -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">📊</span>
                    Dataset
                </h2>
                <div class="card">
                    <h3>Disaster Response Object Detection Dataset</h3>
                    <p>This comprehensive dataset contains annotated images for training object detection models specifically designed for disaster response scenarios. The dataset includes various objects and situations commonly encountered during emergency operations.</p>
                    <a href="https://www.kaggle.com/datasets/rupankarmajumdar/disaster-response-object-detection-dataset"
                       class="kaggle-link" target="_blank">
                       🔗 View Dataset on Kaggle
                    </a>
                </div>
            </div>

            <!-- Methodology Timeline -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">🔬</span>
                    Research Methodology
                </h2>
                <div class="timeline">
                    <div class="timeline-item">
                        <h3 style="color: #adb8e8ff; margin-bottom: 10px;">Phase 1: Baseline Supervised Learning</h3>
                        <p>Implementation of three state-of-the-art YOLO models to establish baseline performance metrics.</p>
                    </div>
                    <div class="timeline-item">
                        <h3 style="color: #afbaecff; margin-bottom: 10px;">Phase 2: Semi-Supervised Learning</h3>
                        <p>Leveraging both labeled and unlabeled data to improve model generalization and performance.</p>
                    </div>
                    <div class="timeline-item">
                        <h3 style="color: #b1bae4ff; margin-bottom: 10px;">Phase 3: Self-Supervised Learning</h3>
                        <p>Training models to learn representations from unlabeled data for enhanced feature extraction.</p>
                    </div>
                </div>
            </div>

            <!-- Baseline Models -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">🎯</span>
                    Baseline Supervised Models
                </h2>
                <div class="model-grid">
                    <div class="model-card">
                        <h3>YOLOv10</h3>
                        <p>The first baseline model implementing YOLOv10 architecture for disaster response object detection.</p>
                        <div style="margin: 15px 0;">
                            <span class="tag">Baseline</span>
                            <span class="tag">Supervised</span>
                        </div>
                        <a href="https://www.kaggle.com/code/afsinnn/disaster-response-yolov10"
                           class="kaggle-link" target="_blank">
                           📓 View Notebook
                        </a>
                    </div>

                    <div class="model-card">
                        <h3>YOLOv11</h3>
                        <p>Enhanced detection capabilities with YOLOv11 architecture, offering improved accuracy and speed.</p>
                        <div style="margin: 15px 0;">
                            <span class="tag">Baseline</span>
                            <span class="tag">Supervised</span>
                        </div>
                        <a href="https://www.kaggle.com/code/afsinnn/object-detection-yolo11"
                           class="kaggle-link" target="_blank">
                           📓 View Notebook
                        </a>
                    </div>

                    <div class="model-card">
                        <h3>YOLOv12</h3>
                        <p>Latest YOLO architecture implementation providing state-of-the-art performance in object detection.</p>
                        <div style="margin: 15px 0;">
                            <span class="tag">Baseline</span>
                            <span class="tag">Supervised</span>
                        </div>
                        <a href="https://www.kaggle.com/code/afsinnn/disaster-response-work-yolo-12"
                           class="kaggle-link" target="_blank">
                           📓 View Notebook
                        </a>
                    </div>
                </div>
            </div>

            <!-- Advanced Models -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">🧠</span>
                    Advanced Learning Approaches
                </h2>
                <div class="model-grid">
                    <div class="model-card" style="border-top-color: #28a745;">
                        <h3>Semi-Supervised Model</h3>
                        <p>Utilizing both labeled and unlabeled data to enhance model performance and generalization capabilities in disaster scenarios.</p>
                        <div style="margin: 15px 0;">
                            <span class="tag" style="background: #28a745;">Semi-Supervised</span>
                            <span class="tag" style="background: #28a745;">Advanced</span>
                        </div>
                        <a href="semi-supervised-object-detection-for-disaster.ipynb"
                           class="kaggle-link" style="background: #28a745;" target="_blank">
                           📓 View Notebook
                        </a>
                    </div>

                    <div class="model-card" style="border-top-color: #ffc107;">
                        <h3>Self-Supervised Model</h3>
                        <p>Learning robust feature representations from unlabeled data to improve detection accuracy without extensive manual annotation.</p>
                        <div style="margin: 15px 0;">
                            <span class="tag" style="background: #ffc107; color: #333;">Self-Supervised</span>
                            <span class="tag" style="background: #ffc107; color: #333;">Advanced</span>
                        </div>
                        <a href="self-supervised-model-dino-byol.ipynb"
                           class="kaggle-link" style="background: #ffc107; color: #333;" target="_blank">
                           📓 View Notebook
                        </a>
                    </div>
                </div>
            </div>

            <!-- Key Features -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">✨</span>
                    Key Features
                </h2>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;">
                    <div class="card">
                        <h3>🎯 Multi-Model Comparison</h3>
                        <p>Comprehensive analysis across YOLOv10, v11, and v12 architectures</p>
                    </div>
                    <div class="card">
                        <h3>📈 Progressive Learning</h3>
                        <p>From supervised to semi-supervised and self-supervised approaches</p>
                    </div>
                    <div class="card">
                        <h3>🚀 Real-time Detection</h3>
                        <p>Optimized for rapid response in emergency situations</p>
                    </div>
                    <div class="card">
                        <h3>📊 Performance Metrics</h3>
                        <p>Detailed evaluation and comparison of all models</p>
                    </div>
                </div>
            </div>

            <!-- Technologies -->
            <div class="section">
                <h2 class="section-title">
                    <span class="icon">💻</span>
                    Technologies Used
                </h2>
                <div class="info-box" style="border-left-color: #667eea;">
                    <h4 style="color: #667eea;">Tech Stack</h4>
                    <p>
                        <strong>Deep Learning:</strong> PyTorch, Ultralytics YOLO<br>
                        <strong>Computer Vision:</strong> OpenCV, Albumentations<br>
                        <strong>Data Processing:</strong> NumPy, Pandas<br>
                        <strong>Platform:</strong> Kaggle Notebooks, Google Colab<br>
                        <strong>Languages:</strong> Python 3.x
                    </p>
                </div>
            </div>
        </div>

        <!-- Footer -->
        <div class="footer">
            <div class="footer-grid">
                <div>
                    <h3>👨‍🏫 Instructor</h3>
                    <p>
                        <strong>Dr. Mohammad Rifat Ahmmad Rashid</strong><br>
                        Associate Professor<br>
                        Department of Computer Science & Engineering
                    </p>
                </div>
                <div>
                    <h3>👩‍🎓 Student</h3>
                    <p>
                        <strong>Afsin Sultana</strong><br>
                        Student ID: 2022-1-60-113<br>
                        Department of Computer Science & Engineering
                    </p>
                </div>
                <div>
                    <h3>📬 Connect</h3>
                    <p>
                        📧 Kaggle: <a href="https://www.kaggle.com/afsinnn" style="color: #84fab0;">@afsinnn</a><br>
                        🔗 Project Links on Kaggle<br>
                        💡 Open for Collaboration
                    </p>
                </div>
            </div>
            <div style="margin-top: 30px; padding-top: 30px; border-top: 1px solid rgba(255,255,255,0.1);">
                <p style="opacity: 0.8;">
                    ⭐ If you find this project helpful, please star it on GitHub!<br>
                    Made with ❤️ for Disaster Response and Emergency Management
                </p>
            </div>
        </div>
    </div>

</body>
</html>
