---
layout: home

---

**Third-Year Computer Science Student @ University of St Andrews**  
*Dean's List 2025 | First-Class Standing | Seeking Summer 2026 Internships*

Welcome to my technical portfolio! I'm passionate about building software solutions with expertise in Python, C, Java, and C++. I am currently exploring opportunities in a variety of software engineering roles to further develop my programming and technical abilities.

---

##  Education & Background

**University of St Andrews** - B.Sc. Hons Computer Science (Expected 1st, 2027)  
*Dean's List 2025 (82.5%+ average)* | *Modules: Databases, OS, AI, Advanced Networks, Web Dev*

**Previous Education:** Forth Valley College Foundation Apprenticeship in Software Development 
Lornshill Academy: SQA Highers AAABB

---

##  Professional Experience

**BlackRock, Edinburgh** - Spring Internship, Software Engineering (April 2025)  
- Collaborated on financial problem-solving using software tools and data analysis
- Participated in incident management for production financial data pipelines
- Engaged with senior engineers on software-finance intersections

**Palantir Technologies** - Virtual Technology Work Experience (June 2022)  
- Organized and filtered large datasets for mock analysis projects
- Proposed data-driven solutions to real-world problems

---

##  Technical Projects

<div class="project-grid">
{% for project in site.projects %}
  <div class="project-card">
    <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
    <p>{{ project.description }}</p>
    {% if project.technologies %}
    <div class="tech-tags">
      {% for tech in project.technologies %}
      <span class="tech-tag">{{ tech }}</span>
      {% endfor %}
    </div>
    {% endif %}
    {% if project.github_url %}
    <a href="{{ project.github_url }}" class="project-link">View Code →</a>
    {% endif %}
  </div>
{% endfor %}
</div>

---

##  Technical Skills

**Programming:** Python, Java, C, Haskell, JavaScript, PHP, C++  
**Web Development:** HTML/CSS, MySQL, MongoDB, Flask, Node.js  
**Tools & Frameworks:** Git, JUnit, Jupyter, MatPlotLib, Linux

---


<style>
.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 1.5rem;
  margin: 2rem 0;
}

.project-card {
  border: 1px solid #e1e4e8;
  border-radius: 8px;
  padding: 1.5rem;
  transition: transform 0.2s, box-shadow 0.2s;
  background: white;
}

.project-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0,0,0,0.1);
}

.tech-tags {
  margin: 1rem 0;
}

.tech-tag {
  display: inline-block;
  background: #f1f8ff;
  color: #0366d6;
  padding: 0.3rem 0.7rem;
  border-radius: 15px;
  font-size: 0.8rem;
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.project-link {
  color: #0366d6;
  text-decoration: none;
  font-weight: 500;
  display: inline-block;
  margin-top: 0.5rem;
}

.project-link:hover {
  text-decoration: underline;
}

.btn {
  display: inline-block;
  background: #0366d6;
  color: white;
  padding: 0.7rem 1.5rem;
  border-radius: 6px;
  text-decoration: none;
  font-weight: 500;
  margin-right: 1rem;
  margin-bottom: 1rem;
  transition: background 0.2s;
}

.btn:hover {
  background: #0256b9;
  text-decoration: none;
  color: white;
}

.btn-secondary {
  background: #6c757d;
}

.btn-secondary:hover {
  background: #545b62;
}
</style>