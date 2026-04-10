/* =====================================================
   TIMELESS LIVING — Interactive JavaScript
   ===================================================== */

// ---- NAV: scroll + hamburger ----
const navbar = document.getElementById('navbar');
const hamburger = document.getElementById('hamburger');
const navLinks = document.getElementById('nav-links');

window.addEventListener('scroll', () => {
  if (window.scrollY > 60) {
    navbar.classList.add('scrolled');
  } else {
    navbar.classList.remove('scrolled');
  }
}, { passive: true });

hamburger.addEventListener('click', () => {
  hamburger.classList.toggle('open');
  navLinks.classList.toggle('open');
  document.body.style.overflow = navLinks.classList.contains('open') ? 'hidden' : '';
});

// Close mobile menu on link click
navLinks.querySelectorAll('a').forEach(link => {
  link.addEventListener('click', () => {
    hamburger.classList.remove('open');
    navLinks.classList.remove('open');
    document.body.style.overflow = '';
  });
});

// ---- SCROLL ANIMATIONS ----
const observerOptions = {
  threshold: 0.12,
  rootMargin: '0px 0px -40px 0px'
};

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, observerOptions);

// Apply fade-up to key elements
function initScrollAnimations() {
  const targets = [
    '.about-image-col',
    '.about-copy',
    '.service-card',
    '.portfolio-item',
    '.process-step',
    '.contact-left',
    '.contact-right',
    '.testimonial-inner > *',
  ];

  targets.forEach(selector => {
    document.querySelectorAll(selector).forEach((el, i) => {
      el.classList.add('fade-up');
      el.setAttribute('data-delay', Math.min(i + 1, 5));
      observer.observe(el);
    });
  });

  // Process step connector animation
  document.querySelectorAll('.process-step').forEach(step => {
    observer.observe(step);
  });
}

// ---- PORTFOLIO FILTER ----
function initPortfolioFilter() {
  const filterBtns = document.querySelectorAll('.filter-btn');
  const items = document.querySelectorAll('.portfolio-item');

  filterBtns.forEach(btn => {
    btn.addEventListener('click', () => {
      // Update active state
      filterBtns.forEach(b => {
        b.classList.remove('active');
        b.setAttribute('aria-selected', 'false');
      });
      btn.classList.add('active');
      btn.setAttribute('aria-selected', 'true');

      const filter = btn.dataset.filter;

      items.forEach(item => {
        if (filter === 'all' || item.dataset.cat === filter) {
          item.classList.remove('hidden');
          // Re-observe for animation
          item.classList.remove('visible');
          setTimeout(() => item.classList.add('visible'), 50);
        } else {
          item.classList.add('hidden');
        }
      });
    });
  });
}

// ---- CONTACT FORM ----
function initContactForm() {
  const form = document.getElementById('contact-form');
  const successMsg = document.getElementById('form-success');
  const submitBtn = document.getElementById('form-submit');

  if (!form) return;

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    const name = form.name.value.trim();
    const email = form.email.value.trim();
    const message = form.message.value.trim();

    if (!name || !email || !message) {
      // Highlight empty required fields
      [form.name, form.email, form.message].forEach(field => {
        if (!field.value.trim()) {
          field.style.borderColor = 'var(--terra-light)';
          field.addEventListener('input', () => {
            field.style.borderColor = '';
          }, { once: true });
        }
      });
      return;
    }

    // Simulate form submission
    submitBtn.textContent = 'Sending...';
    submitBtn.style.opacity = '0.7';
    submitBtn.disabled = true;

    setTimeout(() => {
      form.reset();
      submitBtn.textContent = 'Send My Inquiry';
      submitBtn.style.opacity = '1';
      submitBtn.disabled = false;
      successMsg.classList.add('visible');
      setTimeout(() => successMsg.classList.remove('visible'), 6000);
    }, 1400);
  });
}

// ---- SMOOTH NAV HIGHLIGHT ----
function initActiveNav() {
  const sections = document.querySelectorAll('section[id]');
  const navLinkEls = document.querySelectorAll('.nav-link');

  const sectionObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const id = entry.target.id;
        navLinkEls.forEach(link => {
          link.style.color = '';
          if (link.getAttribute('href') === `#${id}`) {
            link.style.color = 'var(--charcoal)';
          }
        });
      }
    });
  }, { threshold: 0.4 });

  sections.forEach(s => sectionObserver.observe(s));
}

// ---- PARALLAX (subtle) ----
function initParallax() {
  const heroImg = document.querySelector('.hero-img');
  if (!heroImg) return;

  window.addEventListener('scroll', () => {
    const scrolled = window.scrollY;
    if (scrolled < window.innerHeight) {
      heroImg.style.transform = `scale(1) translateY(${scrolled * 0.2}px)`;
    }
  }, { passive: true });
}

// ---- INIT ----
document.addEventListener('DOMContentLoaded', () => {
  initScrollAnimations();
  initPortfolioFilter();
  initContactForm();
  initActiveNav();
  initParallax();
});
