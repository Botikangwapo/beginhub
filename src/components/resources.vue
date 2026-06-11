<template>
    <section id="resources" class="py-24 px-6 bg-gray-50">
        <div class="mx-auto max-w-7xl">
            <div class="text-center mb-16">
                <span class="text-xs font-bold text-blue-600 uppercase tracking-widest">Master Your Skills</span>
                <h2 class="mt-3 text-4xl font-extrabold text-gray-900">Empowering Web Professionals</h2>
                <p class="mt-4 text-gray-600 max-w-lg mx-auto">
                    A comprehensive platform to test your knowledge, earn certifications, and track your growth in web
                    development.
                </p>
            </div>

            <div class="grid gap-8 lg:grid-cols-2">

                <div class="rounded-3xl bg-white p-8 border border-gray-200 shadow-sm">
                    <div
                        class="flex h-12 w-12 items-center justify-center rounded-2xl bg-blue-600 text-white font-bold text-lg">
                        01</div>
                    <h3 class="mt-6 text-2xl font-bold text-gray-900">Curated Learning Paths</h3>
                    <p class="mt-3 text-gray-500 leading-relaxed">
                        Access structured quiz modules designed to reinforce web principles, from front-end basics to
                        advanced deployment strategies.
                    </p>

                    <div class="mt-8 rounded-2xl bg-blue-50 p-6">
                        <span class="text-xs font-bold text-blue-700 uppercase tracking-wider">What you'll cover</span>
                        <div class="mt-4 grid gap-3 text-sm text-gray-700">
                            <div
                                class="flex items-center gap-3 bg-white p-3 rounded-lg border border-blue-100 shadow-sm">
                                <span class="text-blue-500">✓</span> Core Web Fundamentals
                            </div>
                            <div
                                class="flex items-center gap-3 bg-white p-3 rounded-lg border border-blue-100 shadow-sm">
                                <span class="text-blue-500">✓</span> Interactive Tech Challenges
                            </div>
                            <div
                                class="flex items-center gap-3 bg-white p-3 rounded-lg border border-blue-100 shadow-sm">
                                <span class="text-blue-500">✓</span> Real-time Performance Metrics
                            </div>
                        </div>
                    </div>

                    <div class="mt-8 p-6 rounded-2xl bg-gray-900 text-white">
                        <h4 class="font-bold text-lg">Ready to test your limits?</h4>
                        <p class="text-gray-400 text-sm mt-2 mb-6">Start your journey today and earn badges that prove
                            your expertise.</p>
                        <router-link to="/register"
                            class="block w-full text-center py-3 rounded-xl bg-blue-600 hover:bg-blue-700 transition font-semibold">
                            Get Started Now
                        </router-link>
                    </div>
                </div>

                <div class="grid gap-8">
                    <div class="rounded-3xl bg-white p-8 border border-gray-200 shadow-sm">
                        <div
                            class="flex h-12 w-12 items-center justify-center rounded-2xl bg-emerald-500 text-white font-bold text-lg">
                            02</div>
                        <h3 class="mt-6 text-2xl font-bold text-gray-900">Skill-Based Badges</h3>
                        <p class="mt-3 text-gray-500">
                            Stay motivated by earning badges as you master new topics. Your dashboard provides
                            personalized feedback on where to improve next.
                        </p>
                    </div>

                    <div class="rounded-3xl bg-white p-8 border border-gray-200 shadow-sm">
                        <div
                            class="flex h-12 w-12 items-center justify-center rounded-2xl bg-amber-500 text-white font-bold text-lg">
                            03</div>
                        <h3 class="mt-6 text-2xl font-bold text-gray-900">Professional Certifications</h3>
                        <p class="mt-3 text-gray-500">
                            Upon course completion, receive a verified digital certification that you can showcase on
                            your portfolio or LinkedIn profile.
                        </p>

                        <div class="mt-6 p-5 border border-gray-100 rounded-xl bg-gray-50">
                            <p class="text-xs font-semibold text-gray-400 uppercase">Certificate Preview</p>
                            <div class="mt-3">
                                <p class="font-bold text-gray-800">Quiz Mastery Certificate</p>
                                <p class="text-sm text-gray-500">Awarded for excellence in Web Development.</p>
                                <p class="mt-3 text-blue-600 font-mono font-bold tracking-widest">#CERT-2026-WEB</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>