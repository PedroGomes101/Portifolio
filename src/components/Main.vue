<template>
    <canvas id="canvas"></canvas>

    <section id="home" class="hero">
        <div class="hero-inner">
            <img src="./../../public/img.jpg" alt="avatar" class="avatar" aria-hidden="true" />
            <h1>Portfolio</h1>
            <h2>by Pedro Carvalho</h2>

            <nav class="icons-row" aria-hidden="true">
                <a class="social-btn" href="https://github.com/PedroGomes101" aria-label="GitHub">
                    <img :src="github" alt="GitHub" />
                </a>
                <a class="social-btn" href="https://www.instagram.com/pedrog_carvalh" aria-label="Instagram">
                    <img :src="instagram" alt="Instagram" />
                </a>
                <a class="social-btn" href="https://www.linkedin.com/in/pedro-gomes-26383925b" aria-label="LinkedIn">
                    <img :src="linkedin" alt="inkedIn" />
                </a>
            </nav>
        </div>
    </section>

    <section id="cv" class="cv-section">
        <div class="cv-container">
            <div class="cv-grid">
                <!-- Coluna Esquerda -->
                <div class="cv-left">
                    <div class="cv-section">
                        <h3>SKILLS</h3>
                        <div class="skills-grid">
                            <div class="skill-group">
                                <h4>Programming</h4>
                                <div class="skill-item">
                                    <span>JavaScript</span>
                                    <div class="skill-level">
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot"></span>
                                    </div>
                                </div>
                                <div class="skill-item">
                                    <span>Java</span>
                                    <div class="skill-level">
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot"></span>
                                        <span class="dot"></span>
                                    </div>
                                </div>
                                <div class="skill-item">
                                    <span>Python</span>
                                    <div class="skill-level">
                                        <span class="dot filled"></span>
                                        <span class="dot"></span>
                                        <span class="dot"></span>
                                        <span class="dot"></span>
                                        <span class="dot "></span>
                                    </div>
                                </div>
                            </div>
                            
                            <div class="skill-group">
                                <h4>Tools & Systems</h4>
                                <div class="skill-item">
                                    <span>Git</span>
                                    <div class="skill-level">
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot"></span>
                                    </div>
                                </div>
                                <div class="skill-item">
                                    <span>Docker</span>
                                    <div class="skill-level">
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot filled"></span>
                                        <span class="dot"></span>
                                        <span class="dot"></span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Coluna Direita -->
                <div class="cv-right">
                    <div class="cv-section">
                        <h3>EDUCATION</h3>
                        <div class="education-item">
                            <div class="education-header">
                                <h4>Bachelor's in Information System</h4>
                                <span>2023 - in progress</span>
                            </div>
                            <p>Technical University</p>
                            <ul class="achievements">
                                <li>First Class Honours</li>
                                <li>Student Representative</li>
                            </ul>
                        </div>
                         <div class="education-header">
                                <h4>Mini Course: "R PARA INICIANTES"</h4>
                                <span>2021 - 2022</span>
                            </div>
                            <p>Technical University</p>
                            <ul class="achievements">
                                <li>Mini curso basico sobre a linguagem R.</li>
                            </ul>
                        </div>
                        </div>
                    </div>

                    <div class="cv-section">
                        <h3>EXPERIENCE</h3>
                        <div class="experience-item">
                            <div class="experience-header">
                                <h4>Software Developer</h4>
                                <span>2023 - Present</span>
                            </div>
                            <p>Tech Company</p>
                            <ul class="achievements">
                                <li>Developed and maintained full-stack applications</li>
                            </ul>
                        </div>
                    </div>
                </div>
    </section>

    <footer>
        <p>2025 Pedro Carvalho.</p>
    </footer>
</template>

<script>
import github from './icons/github.svg';
import linkedin from './icons/linkedin.svg';
import instagram from './icons/instagram.svg';


export default {
    name: 'Portfolio',
    data() {
        return {
            github,
            linkedin,
            instagram,

        };
    },
    mounted() {
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let particles = [];
        const particleCount = 100;
        const maxDistance = 150;

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.vx = (Math.random() - 0.5) * 0.5;
                this.vy = (Math.random() - 0.5) * 0.5;
                this.radius = Math.random() * 2 + 1;
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;

                if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
                if (this.y < 0 || this.y > canvas.height) this.vy *= -1;
            }

            draw() {
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = 'rgba(255, 255, 255, 0.8)';
                ctx.fill();
            }
        }

        function init() {
            particles = [];
            for (let i = 0; i < particleCount; i++) {
                particles.push(new Particle());
            }
        }

        function connectParticles() {
            for (let i = 0; i < particles.length; i++) {
                for (let j = i + 1; j < particles.length; j++) {
                    const dx = particles[i].x - particles[j].x;
                    const dy = particles[i].y - particles[j].y;
                    const distance = Math.sqrt(dx * dx + dy * dy);

                    if (distance < maxDistance) {
                        const opacity = 1 - (distance / maxDistance);
                        ctx.beginPath();
                        ctx.strokeStyle = `rgba(100, 255, 218, ${opacity * 0.3})`;
                        ctx.lineWidth = 1;
                        ctx.moveTo(particles[i].x, particles[i].y);
                        ctx.lineTo(particles[j].x, particles[j].y);
                        ctx.stroke();
                    }
                }
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            particles.forEach(particle => {
                particle.update();
                particle.draw();
            });

            connectParticles();

            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            init();
        });

        init();
        animate();

        // Smooth scroll
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
    }
}
</script>

