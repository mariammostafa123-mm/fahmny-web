<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>فهمني | Fahemny - ابنِ مشاريعك وسوّق لنفسك تلقائياً</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Cairo Font -->
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&display=swap" rel="stylesheet">
  <!-- React & Babel -->
  <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <style>
    body { font-family: 'Cairo', sans-serif; background-color: #f8fafc; }
    .brand-gradient { background: linear-gradient(135deg, #7C3AED 0%, #4C1D95 100%); }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    const { useState } = React;

    const FahemnyLogo = () => (
      <div className="flex items-center gap-2.5">
        <div className="w-10 h-10 rounded-xl bg-white shadow-md flex items-center justify-center border border-purple-100">
          <svg viewBox="0 0 100 100" className="w-7 h-7">
            <defs>
              <linearGradient id="fGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stopColor="#8B5CF6" />
                <stop offset="100%" stopColor="#4C1D95" />
              </linearGradient>
            </defs>
            <path
              d="M 65 20 H 38 C 30 20 25 25 25 33 V 80 M 25 52 H 55"
              stroke="url(#fGrad)"
              strokeWidth="16"
              strokeLinecap="round"
              strokeLinejoin="round"
              fill="none"
            />
            <circle cx="72" cy="74" r="10" fill="#F59E0B" />
          </svg>
        </div>
        <div>
          <span className="text-xl font-extrabold bg-clip-text text-transparent bg-gradient-to-l from-purple-800 to-indigo-600">
            فَهّمني
          </span>
          <span className="block text-[10px] text-amber-500 font-bold -mt-1 tracking-wider">FAHEMNY.TECH</span>
        </div>
      </div>
    );

    function App() {
      const [activeTab, setActiveTab] = useState('projects');
      const [simModalProject, setSimModalProject] = useState(null);
      const [simStep, setSimStep] = useState(0);

      const [projects, setProjects] = useState([
        {
          id: 1,
          title: 'تصميم وبناء لوحة تحكم تفاعلية (Dashboard UI)',
          track: 'Frontend & UI/UX',
          difficulty: 'متوسط',
          skills: ['React.js', 'Tailwind CSS', 'UI/UX Design'],
          completed: true,
          score: 96,
          description: 'بناء واجهة مستخدم حديثة لتحليل بيانات المبيعات مع تجربة مستخدم سلسة ومتجاوبة.'
        },
        {
          id: 2,
          title: 'تطوير نموذج ذكاء اصطناعي لتصنيف البيانات',
          track: 'AI & Machine Learning',
          difficulty: 'متقدم',
          skills: ['Python', 'Data Analysis', 'Model Training'],
          completed: false,
          score: null,
          description: 'تدريب نموذج عملي على قراءة البيانات وتنظيفها واستخراج التوقعات بدقة عالية.'
        },
        {
          id: 3,
          title: 'بناء تطبيق إدارة مهام تفاعلي مع التحقق من المدخلات',
          track: 'Web Development',
          difficulty: 'مبتدئ',
          skills: ['JavaScript ES6', 'DOM Manipulation', 'HTML5/CSS3'],
          completed: false,
          score: null,
          description: 'تطبيق ويب كامل لإدارة المهام اليومية مع حفظ الحالة والتحقق الفوري من المدخلات.'
        }
      ]);

      const triggerSimulation = (project) => {
        setSimModalProject(project);
        setSimStep(1);
        setTimeout(() => setSimStep(2), 1200);
        setTimeout(() => {
          setSimStep(3);
          setProjects(prev => prev.map(p => p.id === project.id ? { ...p, completed: true, score: 98 } : p));
        }, 2500);
      };

      const completedProjects = projects.filter(p => p.completed);
      const allEarnedSkills = [...new Set(completedProjects.flatMap(p => p.skills))];

      return (
        <div className="min-h-screen flex flex-col">
          {/* Header */}
          <header className="bg-white border-b border-slate-200 sticky top-0 z-30">
            <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
              <FahemnyLogo />
              <div className="flex gap-2 bg-slate-100 p-1 rounded-xl">
                <button
                  onClick={() => setActiveTab('projects')}
                  className={`px-4 py-1.5 rounded-lg text-sm font-bold transition ${activeTab === 'projects' ? 'bg-purple-700 text-white shadow' : 'text-slate-600 hover:text-purple-700'}`}
                >
                  💻 المشاريع العملية
                </button>
                <button
                  onClick={() => setActiveTab('cv')}
                  className={`px-4 py-1.5 rounded-lg text-sm font-bold transition ${activeTab === 'cv' ? 'bg-purple-700 text-white shadow' : 'text-slate-600 hover:text-purple-700'}`}
                >
                  📝 الـ CV التلقائي ({completedProjects.length})
                </button>
                <button
                  onClick={() => setActiveTab('linkedin')}
                  className={`px-4 py-1.5 rounded-lg text-sm font-bold transition ${activeTab === 'linkedin' ? 'bg-purple-700 text-white shadow' : 'text-slate-600 hover:text-purple-700'}`}
                >
                  🚀 شير LinkedIn
                </button>
              </div>
            </div>
          </header>

          {/* Hero Banner */}
          <section className="brand-gradient text-white py-10 px-4">
            <div className="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-between gap-6">
              <div className="max-w-xl">
                <span className="inline-block bg-amber-400 text-slate-900 text-xs font-extrabold px-3 py-1 rounded-full mb-3">
                  🎯 من التدريب العملي لسوق العمل مباشرة
                </span>
                <h1 className="text-2xl md:text-4xl font-extrabold leading-tight mb-3">
                  اشتغل بإيدك على مشاريع حقيقية.. وسيب الـ CV والتسويق علينا!
                </h1>
                <p className="text-purple-100 text-sm md:text-base">
                  بمجرد إنهاء أي مشروع عملي، النظام بيوثق مهاراتك، يحدث الـ CV بتاعك، وينشر إنجازك على LinkedIn عشان الشركات تشوف شغلك فوراً.
                </p>
              </div>
              <button
                onClick={() => {
                  const nextProj = projects.find(p => !p.completed) || projects[0];
                  triggerSimulation(nextProj);
                }}
                className="bg-amber-400 hover:bg-amber-300 text-slate-950 font-extrabold px-6 py-4 rounded-2xl shadow-lg transition transform hover:-translate-y-0.5 whitespace-nowrap"
              >
                ⚡ جرب محاكاة تسليم مشروع فوري
              </button>
            </div>
          </section>

          {/* Main Content */}
          <main className="max-w-6xl mx-auto px-4 py-8 flex-1 w-full">
            {activeTab === 'projects' && (
              <div>
                <h2 className="text-xl font-extrabold text-slate-800 mb-6">💻 المشاريع والتطبيقات الجاهزة للتنفيذ</h2>
                <div className="grid md:grid-cols-3 gap-6">
                  {projects.map(project => (
                    <div key={project.id} className="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm flex flex-col justify-between">
                      <div>
                        <div className="flex justify-between items-center mb-3">
                          <span className="text-xs font-bold bg-purple-50 text-purple-700 px-3 py-1 rounded-full">{project.track}</span>
                          {project.completed ? (
                            <span className="text-xs font-bold bg-emerald-100 text-emerald-700 px-2.5 py-1 rounded-full">✅ مكتمل وموثق ({project.score}%)</span>
                          ) : (
                            <span className="text-xs font-semibold text-slate-400">مستوى: {project.difficulty}</span>
                          )}
                        </div>
                        <h3 className="font-bold text-lg text-slate-800 mb-2">{project.title}</h3>
                        <p className="text-slate-600 text-sm mb-4">{project.description}</p>
                        <div className="flex flex-wrap gap-1.5 mb-6">
                          {project.skills.map(skill => (
                            <span key={skill} className="text-xs bg-slate-100 text-slate-700 px-2.5 py-1 rounded-md font-medium">#{skill}</span>
                          ))}
                        </div>
                      </div>
                      <button
                        onClick={() => triggerSimulation(project)}
                        className={`w-full py-2.5 rounded-xl font-bold text-sm transition ${
                          project.completed
                            ? 'bg-slate-100 text-slate-700 hover:bg-purple-50 hover:text-purple-700'
                            : 'bg-purple-700 hover:bg-purple-800 text-white shadow-md'
                        }`}
                      >
                        {project.completed ? '🔄 إعادة استعراض التوثيق والشير' : '🚀 سلّم المشروع الآن وحدث الـ CV'}
                      </button>
                    </div>
                  ))}
                </div>
              </div>
            )}

            {activeTab === 'cv' && (
              <div className="bg-white rounded-2xl p-8 border border-slate-200 shadow-sm max-w-3xl mx-auto">
                <div className="flex justify-between items-start border-b border-slate-200 pb-6 mb-6">
                  <div>
                    <span className="text-xs font-bold text-purple-700 bg-purple-50 px-3 py-1 rounded-full">CV مُولّد ومُحدث تلقائياً بواسطة فهمني</span>
                    <h2 className="text-2xl font-extrabold text-slate-900 mt-2">ملف الطالب العملي (Live Portfolio & CV)</h2>
                    <p className="text-slate-500 text-sm">كل مشروع بتخلصه بيتحول فوراً لخبرة عملية ومهارات موثقة جاهزة للـ HR</p>
                  </div>
                  <div className="text-left">
                    <span className="bg-emerald-100 text-emerald-800 text-xs font-extrabold px-3 py-1.5 rounded-lg block">✔ موثق 100% عملياً</span>
                  </div>
                </div>

                <div className="mb-6">
                  <h3 className="font-bold text-slate-800 mb-3">🛠️ المهارات المكتسبة والموثقة (Verified Skills):</h3>
                  <div className="flex flex-wrap gap-2">
                    {allEarnedSkills.map(skill => (
                      <span key={skill} className="bg-purple-700 text-white text-xs font-bold px-3 py-1.5 rounded-lg flex items-center gap-1">
                        <span>★</span> {skill}
                      </span>
                    ))}
                  </div>
                </div>

                <div>
                  <h3 className="font-bold text-slate-800 mb-3">📂 المشاريع العملية المنجزة:</h3>
                  <div className="space-y-4">
                    {completedProjects.map(proj => (
                      <div key={proj.id} className="p-4 rounded-xl bg-slate-50 border border-slate-200">
                        <div className="flex justify-between">
                          <h4 className="font-bold text-purple-900">{proj.title}</h4>
                          <span className="text-xs font-bold text-emerald-700">تقييم الأداء: {proj.score}%</span>
                        </div>
                        <p className="text-sm text-slate-600 mt-1">{proj.description}</p>
                      </div>
                    ))}
                  </div>
                </div>
              </div>
            )}

            {activeTab === 'linkedin' && (
              <div className="max-w-xl mx-auto bg-white rounded-2xl p-6 border border-slate-200 shadow-sm">
                <div className="flex items-center gap-3 mb-4">
                  <div className="w-12 h-12 rounded-full bg-purple-700 text-white flex items-center justify-center font-bold text-lg">ط</div>
                  <div>
                    <h4 className="font-bold text-slate-900">بوست LinkedIn الجاهز للنشر التلقائي</h4>
                    <p className="text-xs text-slate-500">يتم نشره بضغطة زر فور اجتياز المشروع لجذب مسؤولي التوظيف (HR)</p>
                  </div>
                </div>
                <div className="bg-slate-50 p-4 rounded-xl border border-slate-200 text-sm text-slate-800 space-y-2 leading-relaxed">
                  <p>سعيد بمشاركة أحدث إنجاز عملي لي على منصة <strong>#فهمني (Fahemny)</strong>! 🚀</p>
                  <p>قمت اليوم بإتمام وتوثيق مشروع: <strong>"{completedProjects[completedProjects.length - 1]?.title}"</strong> بتقييم عملي <strong>{completedProjects[completedProjects.length - 1]?.score}%</strong>.</p>
                  <p>المهارات التي طبقتها عملياً وتمت إضافتها تلقائياً للـ Portfolio الخاص بي:</p>
                  <p className="text-purple-700 font-bold">{completedProjects[completedProjects.length - 1]?.skills.map(s => `#${s.replace(/\s+/g, '')}`).join(' ')}</p>
                  <div className="mt-4 brand-gradient text-white p-4 rounded-xl flex items-center justify-between">
                    <div>
                      <span className="text-amber-300 text-xs font-bold block">شهادة إنجاز مشروع عملي موثق</span>
                      <span className="font-extrabold text-base">{completedProjects[completedProjects.length - 1]?.title}</span>
                    </div>
                    <span className="bg-white/20 px-3 py-1 rounded-lg text-xs font-bold">Fahemny Verified ✓</span>
                  </div>
                </div>
              </div>
            )}
          </main>

          {/* Automation Modal */}
          {simModalProject && (
            <div className="fixed inset-0 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 z-50">
              <div className="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl">
                <h3 className="text-lg font-extrabold text-slate-900 mb-2">⚙️ جاري أتمتة ملفك المهني...</h3>
                <p className="text-xs text-slate-500 mb-5">{simModalProject.title}</p>

                <div className="space-y-4 mb-6">
                  <div className={`p-3 rounded-xl border flex items-center gap-3 ${simStep >= 1 ? 'border-emerald-500 bg-emerald-50 text-emerald-900' : 'border-slate-200'}`}>
                    <span>{simStep >= 1 ? '✅' : '⏳'}</span>
                    <div className="text-sm font-bold">1. فحص الكود وتوثيق المهارات العملية</div>
                  </div>
                  <div className={`p-3 rounded-xl border flex items-center gap-3 ${simStep >= 2 ? 'border-emerald-500 bg-emerald-50 text-emerald-900' : 'border-slate-200'}`}>
                    <span>{simStep >= 2 ? '✅' : '⏳'}</span>
                    <div className="text-sm font-bold">2. إضافة المشروع وتحديث الـ CV تلقائياً</div>
                  </div>
                  <div className={`p-3 rounded-xl border flex items-center gap-3 ${simStep >= 3 ? 'border-emerald-500 bg-emerald-50 text-emerald-900' : 'border-slate-200'}`}>
                    <span>{simStep >= 3 ? '✅' : '⏳'}</span>
                    <div className="text-sm font-bold">3. تجهيز ونشر بوست الإنجاز على LinkedIn</div>
                  </div>
                </div>

                {simStep === 3 && (
                  <div className="flex gap-2">
                    <button
                      onClick={() => { setSimModalProject(null); setActiveTab('cv'); }}
                      className="flex-1 bg-purple-700 text-white py-2.5 rounded-xl font-bold text-sm"
                    >
                      شاهد الـ CV المحدث 📝
                    </button>
                    <button
                      onClick={() => { setSimModalProject(null); setActiveTab('linkedin'); }}
                      className="flex-1 bg-amber-400 text-slate-950 py-2.5 rounded-xl font-bold text-sm"
                    >
                      شاهد بوست LinkedIn 🚀
                    </button>
                  </div>
                )}
              </div>
            </div>
          )}
        </div>
      );
    }

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
  </script>
</body>
</html>
