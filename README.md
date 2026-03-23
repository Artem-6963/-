<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AHPC.DEV Dashboard | Artem Tymchenko</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    
    <script src="https://unpkg.com/lucide@latest"></script>

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        darkBg: '#0f172a',
                        darkCard: '#1e293b',
                        primary: '#10b981',
                    }
                }
            }
        }
    </script>

    <style>
        body { font-family: 'Inter', sans-serif; }
        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(10px); }
    </style>
</head>
<body class="bg-slate-50 dark:bg-darkBg transition-colors duration-300">

    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect } = React;

        function Dashboard() {
            const [isDark, setIsDark] = useState(true);

            useEffect(() => {
                document.documentElement.classList.toggle('dark', isDark);
            }, [isDark]);

            const stats = [
                { label: 'Курс', value: '3', sub: 'Информационные системы' },
                { label: 'Группа', value: '202PO', sub: 'АВПК / AHPC' },
                { label: 'Локация', value: 'Актобе', sub: 'Казахстан' },
                { label: 'Стек', value: 'Frontend', sub: 'React + Tailwind' }
            ];

            return (
                <div className="min-h-screen flex text-slate-800 dark:text-slate-100">
                    
                    {/* Sidebar */}
                    <aside className="w-64 fixed h-full bg-white dark:bg-darkCard border-r border-slate-200 dark:border-slate-800 p-6 flex flex-col">
                        <div className="flex items-center gap-3 mb-10">
                            <div className="w-10 h-10 bg-primary rounded-xl flex items-center justify-center text-white font-bold shadow-lg shadow-primary/20">A</div>
                            <span className="text-xl font-bold tracking-tight">AHPC.DEV</span>
                        </div>

                        <nav className="flex-1 space-y-2">
                            <button className="w-full flex items-center gap-3 px-4 py-3 rounded-xl bg-primary/10 text-primary font-medium text-sm">
                                <i data-lucide="layout-dashboard" className="w-5 h-5"></i> Дашборд
                            </button>
                            <button className="w-full flex items-center gap-3 px-4 py-3 rounded-xl text-slate-500 hover:bg-slate-100 dark:hover:bg-slate-800/50 transition-all text-sm">
                                <i data-lucide="code" className="w-5 h-5"></i> Проекты
                            </button>
                            <button className="w-full flex items-center gap-3 px-4 py-3 rounded-xl text-slate-500 hover:bg-slate-100 dark:hover:bg-slate-800/50 transition-all text-sm">
                                <i data-lucide="user" className="w-5 h-5"></i> Профиль
                            </button>
                        </nav>

                        <div className="mt-auto p-4 bg-slate-50 dark:bg-slate-800/50 rounded-2xl border border-slate-100 dark:border-slate-800">
                            <p className="text-xs font-bold text-primary mb-1 uppercase tracking-tighter">Студент</p>
                            <p className="text-sm font-bold truncate">Artem Tymchenko</p>
                        </div>
                    </aside>

                    {/* Main Content */}
                    <main className="ml-64 flex-1 p-10">
                        <header className="flex justify-between items-center mb-12">
                            <div>
                                <h1 className="text-3xl font-bold">Главная страница</h1>
                                <p className="text-slate-500 mt-1">Добро пожаловать в систему управления проектами</p>
                            </div>

                            <div className="flex gap-4">
                                <button 
                                    onClick={() => setIsDark(!isDark)}
                                    className="p-3 bg-white dark:bg-darkCard border border-slate-200 dark:border-slate-800 rounded-2xl hover:shadow-xl transition-all"
                                >
                                    {isDark ? <i data-lucide="sun" className="text-yellow-400"></i> : <i data-lucide="moon" className="text-indigo-500"></i>}
                                </button>
                                <div className="flex items-center gap-3 bg-white dark:bg-darkCard border border-slate-200 dark:border-slate-800 px-4 py-2 rounded-2xl">
                                    <div className="w-8 h-8 rounded-full bg-slate-200 dark:bg-slate-700"></div>
                                    <span className="text-sm font-medium">Artem T.</span>
                                </div>
                            </div>
                        </header>

                        {/* Stats Grid */}
                        <div className="grid grid-cols-4 gap-6 mb-10">
                            {stats.map(s => (
                                <div key={s.label} className="p-6 bg-white dark:bg-darkCard rounded-[2rem] border border-slate-200 dark:border-slate-800 shadow-sm hover:border-primary transition-all group">
                                    <p className="text-sm text-slate-500 mb-1">{s.label}</p>
                                    <h3 className="text-2xl font-black group-hover:text-primary transition-colors">{s.value}</h3>
                                    <p className="text-[10px] uppercase font-bold text-slate-400 mt-2 tracking-widest">{s.sub}</p>
                                </div>
                            ))}
                        </div>

                        {/* Middle Section */}
                        <div className="grid grid-cols-3 gap-6">
                            <div className="col-span-2 p-8 bg-white dark:bg-darkCard rounded-[2.5rem] border border-slate-200 dark:border-slate-800 relative overflow-hidden">
                                <div className="flex justify-between items-center mb-8">
                                    <h3 className="text-xl font-bold">Прогресс обучения</h3>
                                    <span className="text-xs text-primary bg-primary/10 px-3 py-1 rounded-full font-bold uppercase">В процессе</span>
                                </div>
                                
                                {/* Имитация графика */}
                                <div className="flex items-end gap-3 h-48">
                                    {[40, 70, 45, 90, 65, 80, 55, 95, 70, 85].map((h, i) => (
                                        <div key={i} className="flex-1 bg-slate-100 dark:bg-slate-800 rounded-t-lg relative group">
                                            <div 
                                                className="absolute bottom-0 w-full bg-primary rounded-t-lg transition-all duration-1000 group-hover:bg-emerald-400" 
                                                style={{ height: h + '%' }}
                                            ></div>
                                        </div>
                                    ))}
                                </div>
                                <div className="flex justify-between mt-4 text-[10px] font-bold text-slate-400 uppercase tracking-widest px-2">
                                    <span>Янв</span><span>Фев</span><span>Мар</span><span>Апр</span><span>Май</span><span>Июн</span>
                                </div>
                            </div>

                            <div className="p-8 bg-primary rounded-[2.5rem] text-white shadow-2xl shadow-primary/30 flex flex-col">
                                <h3 className="text-xl font-bold mb-4 italic">Задание месяца</h3>
                                <p className="text-emerald-100 text-sm leading-relaxed mb-8">
                                    Разработать дашборд главную страницу на любую тематику. Техстек: React 18 + Vite, Tailwind CSS.
                                </p>
                                <div className="mt-auto bg-white/20 p-4 rounded-2xl backdrop-blur-md border border-white/20">
                                    <p className="text-[10px] font-black uppercase mb-2">Дедлайн</p>
                                    <p className="text-2xl font-bold">31 Марта</p>
                                </div>
                            </div>
                        </div>
                    </main>
                </div>
            );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<Dashboard />);

        // Инициализация иконок после рендера
        setTimeout(() => lucide.createIcons(), 500);
    </script>
</body>
</html>
