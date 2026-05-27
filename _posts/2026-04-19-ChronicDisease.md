---
layout: post                  
title: "HealthGuard AI"  
date: 2026-04-19 18:26:23+08:00  
categories: ["Portfolio"]  # 对应分类
tags: ["PM","Portfolio"]  # 细化主题，方便搜索（3-5个）
# cover: /assets/images/covers/文章封面图.jpg
---

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HealthGuard Agent</title>
    <script type="module" src="https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f8f9fa;
        }
        
        h1 {
            font-size: 2.2rem;
            color: #2c3e50;
            text-align: center;
            margin-bottom: 10px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
        }
        
        h2 {
            font-size: 1.8rem;
            color: #2c3e50;
            margin: 40px 0 20px;
            padding-left: 10px;
            border-left: 4px solid #3498db;
        }
        
        h3 {
            font-size: 1.4rem;
            color: #34495e;
            margin: 25px 0 15px;
        }
        
        h4 {
            font-size: 1.2rem;
            color: #34495e;
            margin: 20px 0 10px;
        }
        
        .subtitle {
            text-align: center;
            color: #7f8c8d;
            font-size: 1.1rem;
            margin-bottom: 30px;
        }
        
        .section {
            background: white;
            border-radius: 8px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
            font-size: 0.95rem;
        }
        
        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #e0e0e0;
        }
        
        th {
            background-color: #f8f9fa;
            font-weight: 600;
            color: #2c3e50;
        }
        
        tr:hover {
            background-color: #f8f9fa;
        }
        
        .mermaid {
            margin: 20px 0;
            display: flex;
            justify-content: center;
        }

        .mermaid img {
            max-width: 100%;
            height: auto;
            display: block;
        }
        
        .code-block {
            background-color: #f8f9fa;
            border: 1px solid #e0e0e0;
            border-radius: 4px;
            padding: 15px;
            margin: 15px 0;
            overflow-x: auto;
            font-family: "Consolas", "Monaco", monospace;
            font-size: 0.9rem;
            line-height: 1.5;
        }
        
        .highlight {
            background-color: #e3f2fd;
            padding: 2px 4px;
            border-radius: 3px;
        }
        
        .card-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }
        
        .card {
            background: white;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            border-top: 3px solid #3498db;
        }
        
        .card h4 {
            margin-top: 0;
            color: #2c3e50;
        }
        
        @media (max-width: 768px) {
            body {
                padding: 10px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            h2 {
                font-size: 1.5rem;
            }
            
            .section {
                padding: 15px;
            }
            
            table {
                font-size: 0.85rem;
            }
            
            th, td {
                padding: 8px 10px;
            }
        }
    </style>
</head>
<body>
    <h1>糖尿病患者全周期管理智能体</h1>    
    <div class="section">
        <h2>AI产品生命周期总览</h2>
        <div class="mermaid">
        graph LR
        A[需求与市场分析] --> B[产品定义与AI策略设计]
        B --> C[技术架构与数据准备]
        C --> D[模型训练与效果评估]
        D --> E[灰度发布与A/B测试]
        E --> F[全量上线与运营]
        F --> G[数据闭环与持续迭代]
        G --> B
        </div>
    </div>
    
    <div class="section">
        <h2>1. 需求与市场分析阶段</h2>        
        <h3>1.1 用户研究与痛点量化</h3>
        <table>
            <tr>
                <th>用户角色</th>
                <th>核心痛点</th>
                <th>量化数据</th>
                <th>验证方法</th>
            </tr>
            <tr>
                <td>2型糖尿病患者</td>
                <td>1. 用药依从性差<br>2. 饮食运动无科学指导<br>3. 异常指标发现不及时</td>
                <td>1. 全国平均依从性59%<br>2. 并发症发生率30%<br>3. 年均医疗支出12800元</td>
                <td>深度访谈20人+问卷300份</td>
            </tr>
            <tr>
                <td>内分泌科医生</td>
                <td>1. 门诊时间不足(平均8分钟/人)<br>2. 院外患者数据缺失<br>3. 随访效率极低</td>
                <td>1. 日均随访≤20人<br>2. 30%患者失访<br>3. 80%时间用于重复工作</td>
                <td>访谈5名三甲医院医生</td>
            </tr>
            <tr>
                <td>医疗机构</td>
                <td>1. 慢病管理成本高<br>2. 并发症预防困难<br>3. 医保支出压力大</td>
                <td>1. 慢病占医保支出60%<br>2. 并发症治疗成本是预防的10倍</td>
                <td>行业报告+医院数据</td>
            </tr>
        </table>
        
        <h3>1.2 竞品分析</h3>
        <table>
            <tr>
                <th>竞品</th>
                <th>核心功能</th>
                <th>技术水平</th>
                <th>核心缺陷</th>
                <th>我方差异化</th>
            </tr>
            <tr>
                <td>平安好医生</td>
                <td>在线问诊+用药提醒</td>
                <td>被动问答+规则引擎</td>
                <td>无主动干预，AI能力弱</td>
                <td>主动式AI Agent+多模态数据处理</td>
            </tr>
            <tr>
                <td>糖护士</td>
                <td>血糖记录+社区</td>
                <td>纯工具+人工运营</td>
                <td>无AI分析，无医生端</td>
                <td>AI风险预警+医生智能工作台</td>
            </tr>
            <tr>
                <td>微医</td>
                <td>互联网医院+慢病管理</td>
                <td>人工为主+AI辅助</td>
                <td>成本高，覆盖有限</td>
                <td>低成本规模化+数据闭环</td>
            </tr>
        </table>
        
        <h3>1.3 市场与合规分析</h3>
        <ul>
            <li><strong>市场规模</strong>：中国数字疗法市场2026年达1200亿元，年增长率35%</li>
            <li><strong>政策支持</strong>：《健康中国2030》明确要求加强慢病管理，NMPA已批准多款数字疗法产品</li>
            <li><strong>合规要求</strong>：需通过NMPA二类医疗器械备案，符合《个人信息保护法》医疗数据要求</li>
        </ul>
    </div>
    
    <div class="section">
        <h2>2. 产品定义与AI策略设计阶段</h2>        
        <h3>2.1 产品核心定位</h3>
        <p>用自主AI Agent实现从"被动咨询"到"主动干预"的慢病管理革命，打造医生的"数字助手"和患者的"私人健康管家"</p>
        
        <h3>2.2 核心AI能力定义</h3>
        <div class="mermaid">
            <img src="/assets/chronic-assistant-1.png?t=20260528" 
     alt="RAG知识库构建策略图" 
     style="opacity: 1 !important; animation: none !important; display: block !important;">
        </div>
        
        <h3>2.3 AI核心策略设计</h3>
        
        <h4>🔹 Prompt工程策略</h4>
        <div class="code-block">
系统提示词：
你是一名专业的内分泌科医生助手，基于最新的《中国2型糖尿病防治指南(2026年版)》回答问题。
必须遵守以下规则：
1. 所有回答必须引用临床指南或权威医学文献
2. 禁止提供诊断和治疗建议，只能提供健康指导
3. 遇到紧急情况立即引导用户联系医生或拨打120
4. 对于不确定的问题，明确说明"无法回答，请咨询专业医生"
5. 回答语言要通俗易懂，避免使用专业术语
        </div>
        
        <h4>🔹 RAG知识库构建策略</h4>
        <div class="mermaid">
            <img src="/assets/chronicdisease-1.png" alt="RAG知识库构建策略图" />
        </div>
        
        <h4>🔹 风险分级与干预策略</h4>
        <table>
            <tr>
                <th>风险等级</th>
                <th>血糖范围(mmol/L)</th>
                <th>干预措施</th>
                <th>响应时间</th>
            </tr>
            <tr>
                <td>正常</td>
                <td>3.9-7.0(空腹)<br>4.4-10.0(餐后)</td>
                <td>生成个性化饮食/运动建议</td>
                <td>实时</td>
            </tr>
            <tr>
                <td>低风险</td>
                <td>7.0-10.0(空腹)<br>10.0-13.9(餐后)</td>
                <td>AI自动干预，提醒调整用药/饮食</td>
                <td>5分钟内</td>
            </tr>
            <tr>
                <td>中风险</td>
                <td>10.0-13.9(空腹)<br>13.9-16.7(餐后)</td>
                <td>AI干预+推送医生，24小时内随访</td>
                <td>1小时内</td>
            </tr>
            <tr>
                <td>高风险</td>
                <td>≥13.9(空腹)<br>≥16.7(餐后)</td>
                <td>立即推送医生+短信预警+电话通知</td>
                <td>1分钟内</td>
            </tr>
        </table>
        
        <h4>🔹 异常兜底流程</h4>
        <div class="mermaid">
        graph LR
        A[用户请求] --> B[AI处理]
        B --> C{处理成功?}
        C --> 是 --> D{回答准确?}
        D --> 是 --> E[正常输出]
        D --> 否 --> F[输出标准兜底话术]
        C --> 否 --> G[系统异常提示]
        F --> H[引导人工服务]
        G --> H
        H --> I[记录异常日志]
        I --> J[模型迭代优化]
        </div>
    </div>
    
    <div class="section">
        <h2>3. 技术架构与数据准备阶段</h2>
        
        <h3>3.1 工业级系统架构</h3>
        <div class="mermaid">
        graph TD
        subgraph 前端层
        A[患者端App(React Native)]
        B[医生端Web(Vue3)]
        C[智能硬件SDK]
        end
        subgraph 应用层
        D[API网关]
        E[智能体引擎(LangChain)]
        F[多模态处理模块]
        G[数据安全网关]
        H[用户管理系统]
        end
        subgraph 模型层
        I[医疗大模型(ChatGLM-Med-6B)]
        J[时序预测模型(LSTM)]
        K[风险评估模型(XGBoost)]
        L[RAG检索引擎]
        end
        subgraph 数据层
        M[患者数据库(PostgreSQL)]
        N[向量数据库(Pinecone)]
        O[临床知识库]
        P[隐私计算模块]
        end
        subgraph 基础设施层
        Q[云服务器(AWS/阿里云)]
        R[容器化部署(Docker/K8s)]
        S[监控与告警系统]
        T[日志系统]
        end
        </div>
        
        <h3>3.2 数据准备方案（合规优先）</h3>
        <table>
            <tr>
                <th>数据类型</th>
                <th>数据来源</th>
                <th>数据量</th>
                <th>处理方式</th>
                <th>合规要求</th>
            </tr>
            <tr>
                <td>临床指南</td>
                <td>中华医学会、ADA</td>
                <td>50+篇</td>
                <td>PDF转文本+语义分块</td>
                <td>公开数据，无版权问题</td>
            </tr>
            <tr>
                <td>脱敏病历</td>
                <td>MIMIC-IV公开数据集</td>
                <td>5000份</td>
                <td>结构化处理+去标识化</td>
                <td>HIPAA合规</td>
            </tr>
            <tr>
                <td>模拟患者数据</td>
                <td>生成式AI</td>
                <td>10万条</td>
                <td>基于真实数据分布生成</td>
                <td>无隐私风险</td>
            </tr>
            <tr>
                <td>用户行为数据</td>
                <td>产品埋点</td>
                <td>实时采集</td>
                <td>匿名化处理</td>
                <td>用户授权同意</td>
            </tr>
        </table>
        
        <h3>3.3 技术选型与成本估算</h3>
        <table>
            <tr>
                <th>模块</th>
                <th>技术选型</th>
                <th>成本(月)</th>
                <th>说明</th>
            </tr>
            <tr>
                <td>大模型</td>
                <td>ChatGLM-Med-6B(本地部署)</td>
                <td>500元</td>
                <td>开源医疗专用模型，成本低</td>
            </tr>
            <tr>
                <td>向量数据库</td>
                <td>Pinecone免费版</td>
                <td>0元</td>
                <td>支持10万向量，足够MVP使用</td>
            </tr>
            <tr>
                <td>云服务器</td>
                <td>阿里云ECS(4核8G)</td>
                <td>200元</td>
                <td>满足1000用户并发</td>
            </tr>
            <tr>
                <td>其他</td>
                <td>域名、SSL证书等</td>
                <td>50元</td>
                <td>基础运维成本</td>
            </tr>
            <tr>
                <td><strong>总计</strong></td>
                <td></td>
                <td><strong>750元/月</strong></td>
                <td>低成本可落地</td>
            </tr>
        </table>
    </div>
    
    <div class="section">
        <h2>4. 模型训练与效果评估阶段</h2>        
        <h3>4.1 三层评估体系</h3>
        
        <h4>🔹 技术指标层</h4>
        <table>
            <tr>
                <th>指标</th>
                <th>目标值</th>
                <th>评估方法</th>
                <th>优化策略</th>
            </tr>
            <tr>
                <td>意图识别准确率</td>
                <td>≥95%</td>
                <td>500条标注测试集</td>
                <td>增加医疗领域样本</td>
            </tr>
            <tr>
                <td>回答相关性</td>
                <td>≥90%</td>
                <td>BLEU-4+ROUGE-L</td>
                <td>优化RAG检索策略</td>
            </tr>
            <tr>
                <td>响应时间</td>
                <td>&lt;2秒</td>
                <td>100并发压力测试</td>
                <td>模型蒸馏+缓存</td>
            </tr>
            <tr>
                <td>幻觉率</td>
                <td>&lt;3%</td>
                <td>3名医生交叉评审</td>
                <td>知识图谱约束+事实校验</td>
            </tr>
            <tr>
                <td>风险预警准确率</td>
                <td>≥98%</td>
                <td>历史异常数据测试</td>
                <td>调整阈值+特征工程</td>
            </tr>
        </table>
        
        <h4>🔹 业务效果层（用户价值）</h4>
        <table>
            <tr>
                <th>指标</th>
                <th>基线值</th>
                <th>目标值</th>
                <th>评估周期</th>
                <th>数据来源</th>
            </tr>
            <tr>
                <td>用药依从性</td>
                <td>59%</td>
                <td>≥84%</td>
                <td>1个月</td>
                <td>用药记录统计</td>
            </tr>
            <tr>
                <td>血糖达标率</td>
                <td>45%</td>
                <td>≥65%</td>
                <td>3个月</td>
                <td>生化检测数据</td>
            </tr>
            <tr>
                <td>医生随访效率</td>
                <td>20人/天</td>
                <td>≥50人/天</td>
                <td>1个月</td>
                <td>医生操作日志</td>
            </tr>
            <tr>
                <td>患者满意度</td>
                <td>3.2/5</td>
                <td>≥4.5/5</td>
                <td>2周</td>
                <td>问卷调查</td>
            </tr>
            <tr>
                <td>并发症发生率</td>
                <td>30%</td>
                <td>≤21%</td>
                <td>1年</td>
                <td>医院随访数据</td>
            </tr>
        </table>
        
        <h4>🔹 商业价值层（可持续性）</h4>
        <table>
            <tr>
                <th>指标</th>
                <th>目标值</th>
                <th>计算方法</th>
            </tr>
            <tr>
                <td>单用户医疗支出降低</td>
                <td>≥30%</td>
                <td>(干预前-干预后)/干预前</td>
            </tr>
            <tr>
                <td>月留存率</td>
                <td>≥80%</td>
                <td>月活跃用户/总用户</td>
            </tr>
            <tr>
                <td>付费转化率</td>
                <td>≥15%</td>
                <td>付费用户/活跃用户</td>
            </tr>
        </table>
        
        <h3>4.2 模型迭代流程</h3>
        <div class="mermaid">
        graph LR
        A[模型初始版本] --> B[离线评估]
        B --> C{通过?}
        C --> 否 --> D[模型优化]
        C --> 是 --> E[灰度发布]
        E --> F[线上A/B测试]
        F --> G{效果显著?}
        G --> 否 --> D
        G --> 是 --> H[全量上线]
        H --> I[线上数据收集]
        I --> J[标注与分析]
        J --> D
        </div>
    </div>
    
    <div class="section">
        <h2>5. 灰度发布与A/B测试阶段</h2>
        
        <h3>5.1 灰度发布计划</h3>
        <table>
            <tr>
                <th>阶段</th>
                <th>用户规模</th>
                <th>发布时间</th>
                <th>核心目标</th>
            </tr>
            <tr>
                <td>内部测试</td>
                <td>10人(团队成员)</td>
                <td>第76-80天</td>
                <td>功能测试+Bug修复</td>
            </tr>
            <tr>
                <td>种子用户</td>
                <td>100人(内分泌科患者)</td>
                <td>第81-85天</td>
                <td>用户体验测试+模型调优</td>
            </tr>
            <tr>
                <td>小范围灰度</td>
                <td>500人</td>
                <td>第86-90天</td>
                <td>稳定性测试+效果验证</td>
            </tr>
            <tr>
                <td>全量上线</td>
                <td>不限</td>
                <td>第91天</td>
                <td>正式运营</td>
            </tr>
        </table>
        
        <h3>5.2 A/B测试实验设计</h3>
        <table>
            <tr>
                <th>实验名称</th>
                <th>实验组</th>
                <th>对照组</th>
                <th>样本量</th>
                <th>实验周期</th>
                <th>核心指标</th>
            </tr>
            <tr>
                <td>AI提醒效果</td>
                <td>AI个性化提醒</td>
                <td>普通定时提醒</td>
                <td>各200人</td>
                <td>4周</td>
                <td>用药依从性</td>
            </tr>
            <tr>
                <td>RAG问答效果</td>
                <td>RAG增强回答</td>
                <td>纯大模型回答</td>
                <td>各100人</td>
                <td>2周</td>
                <td>回答准确率+用户满意度</td>
            </tr>
            <tr>
                <td>风险预警效果</td>
                <td>AI自动预警</td>
                <td>人工预警</td>
                <td>各100人</td>
                <td>4周</td>
                <td>预警响应时间+并发症发生率</td>
            </tr>
        </table>
        
        <h3>5.3 实验结果示例</h3>
        <table>
            <tr>
                <th>实验名称</th>
                <th>实验组</th>
                <th>对照组</th>
                <th>提升幅度</th>
                <th>统计显著性</th>
            </tr>
            <tr>
                <td>AI提醒效果</td>
                <td>84%</td>
                <td>62%</td>
                <td>+35.5%</td>
                <td>p&lt;0.001</td>
            </tr>
            <tr>
                <td>RAG问答效果</td>
                <td>92%</td>
                <td>78%</td>
                <td>+17.9%</td>
                <td>p&lt;0.01</td>
            </tr>
            <tr>
                <td>风险预警效果</td>
                <td>1分钟</td>
                <td>30分钟</td>
                <td>-96.7%</td>
                <td>p&lt;0.001</td>
            </tr>
        </table>
    </div>
    
    <div class="section">
        <h2>6. 全量上线与运营阶段</h2>
        
        <h3>6.1 运营策略</h3>
        <ul>
            <li><strong>医生端</strong>：提供免费使用+培训，建立医生激励机制</li>
            <li><strong>患者端</strong>：健康积分体系，连续使用可兑换体检服务</li>
            <li><strong>合作渠道</strong>：与医院、社区卫生服务中心、保险公司合作</li>
        </ul>
        
        <h3>6.2 监控与告警体系</h3>
        <table>
            <tr>
                <th>监控维度</th>
                <th>监控指标</th>
                <th>告警阈值</th>
                <th>响应时间</th>
            </tr>
            <tr>
                <td>系统稳定性</td>
                <td>接口成功率</td>
                <td>&lt;99.9%</td>
                <td>5分钟</td>
            </tr>
            <tr>
                <td>模型性能</td>
                <td>响应时间</td>
                <td>&gt;3秒</td>
                <td>10分钟</td>
            </tr>
            <tr>
                <td>业务指标</td>
                <td>日活跃用户</td>
                <td>下降20%</td>
                <td>1小时</td>
            </tr>
            <tr>
                <td>安全指标</td>
                <td>异常访问次数</td>
                <td>&gt;100次/小时</td>
                <td>立即</td>
            </tr>
        </table>
    </div>
    
    <div class="section">
        <h2>7. 数据闭环与持续迭代阶段</h2>
        
        <h3>7.1 数据闭环流程</h3>
        <div class="mermaid">
        graph LR
        A[用户使用产品] --> B[产生行为数据]
        B --> C[数据采集与清洗]
        C --> D[数据分析与挖掘]
        D --> E[发现问题与机会]
        E --> F[产品迭代优化]
        F --> A
        </div>
        
        <h3>7.2 迭代路线图</h3>
        <table>
            <tr>
                <th>版本</th>
                <th>发布时间</th>
                <th>核心功能</th>
            </tr>
            <tr>
                <td>MVP</td>
                <td>第90天</td>
                <td>用药提醒+数据解读+基础问答</td>
            </tr>
            <tr>
                <td>V1.0</td>
                <td>第120天</td>
                <td>风险预警+医生端+医患同步</td>
            </tr>
            <tr>
                <td>V1.5</td>
                <td>第180天</td>
                <td>多智能体协作(营养师+运动教练)</td>
            </tr>
            <tr>
                <td>V2.0</td>
                <td>第270天</td>
                <td>端侧AI+智能硬件集成</td>
            </tr>
            <tr>
                <td>V2.5</td>
                <td>第360天</td>
                <td>医保对接+商业化功能</td>
            </tr>
        </table>
    </div>
    
    
    <footer style="text-align: center; margin-top: 50px; padding: 20px; color: #7f8c8d; border-top: 1px solid #eee;">
    </footer>
</body>
</html>