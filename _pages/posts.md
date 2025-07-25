---
title: "Blog"
permalink: /posts/
layout: single
author_profile: true
---

{% include group-by-array collection=site.posts field="tags" %}
{% assign series_posts = site.posts | where_exp: "post", "post.series" %}
{% assign series_names = series_posts | map: "series" | uniq | sort %}

<div class="series-filter-container">
  <h3 style="margin-top:0">Filter by Series:</h3>
  <div class="series-buttons">
    <button class="series-btn active" data-series="all">All Posts</button>
    {% for series in series_names %}
      <button class="series-btn" data-series="{{ series | slugify }}">{{ series | replace: "-", " " | titleize }}</button>
    {% endfor %}
  </div>
</div>

<div class="posts-container">
  {% for post in site.posts %}
    <article class="post-item" data-tags="{% for tag in post.tags %}{{ tag | slugify }} {% endfor %}" data-series="{{ post.series | slugify }}">
      <h4 style="margin-top:0px"><a href="{{ post.url }}">{{ post.title }}</a></h4>
      <p class="post-meta">
        <time datetime="{{ post.date | date_to_xmlschema }}">
          {{ post.date | date: "%B %d, %Y" }}
        </time>
        {% if post.series %}
          <span class="post-series">Series: {{ post.series | replace: "-", " " | titleize }}</span>
        {% endif %}
      </p>
      {% if post.excerpt %}
        <p style="font-size:.85em">{{ post.excerpt }}</p>
      {% endif %}
    </article>
  {% endfor %}
</div>

<div class="tag-filter-container">
  <button class="filter-toggle" onclick="toggleFilter()">
    <span class="toggle-text">Show Tag Filter</span>
    <span class="toggle-icon">▼</span>
  </button>
  
  <div class="filter-content" id="filterContent" style="display: none;">
    <h3>Filter by Tag:</h3>
    <div class="tag-buttons">
      <button class="tag-btn active" data-tag="all">All Tags</button>
      {% for tag in group_names %}
        <button class="tag-btn" data-tag="{{ tag | slugify }}">{{ tag }}</button>
      {% endfor %}
    </div>
  </div>
</div>

<style>
.series-filter-container {
  padding: 1rem;
  border-radius: 5px;
}

.series-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.series-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #bbdefb;
  background: white;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.2s;
}

.series-btn:hover {
  background: #f3e5f5;
}

.series-btn.active {
  background: #1976d2;
  color: white;
  border-color: #1976d2;
}

.tag-filter-container {
  margin-top: 3rem;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 5px;
  border: 1px solid #e9ecef;
}

.filter-toggle {
  width: 100%;
  padding: 0.75rem 1rem;
  background: white;
  border: 1px solid #ddd;
  border-radius: 5px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1rem;
  transition: all 0.2s;
}

.filter-toggle:hover {
  background: #f8f9fa;
}

.toggle-icon {
  transition: transform 0.2s;
}

.filter-content {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #e9ecef;
}

.tag-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.tag-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #ddd;
  background: white;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.2s;
}

.tag-btn:hover {
  background: #e9ecef;
}

.tag-btn.active {
  background: #007bff;
  color: white;
  border-color: #007bff;
}

.post-item {
  margin-bottom: 2rem;
  padding: 1rem;
  border: 1px solid #eee;
  border-radius: 5px;
  transition: opacity 0.3s;
}

.post-item.hidden {
  display: none;
}

.post-meta {
  color: #666;
  font-size: 0.9rem;
  margin: 0.5rem 0;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.post-series {
  display: inline-block;
  background: #e3f2fd;
  color: #1976d2;
  padding: 0.2rem 0.5rem;
  border-radius: 10px;
  font-size: 0.8rem;
  font-weight: 500;
}


</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const seriesButtons = document.querySelectorAll('.series-btn');
  const tagButtons = document.querySelectorAll('.tag-btn');
  const postItems = document.querySelectorAll('.post-item');

  // Series filtering
  seriesButtons.forEach(button => {
    button.addEventListener('click', function() {
      const selectedSeries = this.getAttribute('data-series');
      
      // Update active button
      seriesButtons.forEach(btn => btn.classList.remove('active'));
      this.classList.add('active');
      
      // Reset tag filter
      tagButtons.forEach(btn => btn.classList.remove('active'));
      document.querySelector('[data-tag="all"]').classList.add('active');
      
      // Filter posts by series
      postItems.forEach(post => {
        const postSeries = post.getAttribute('data-series');
        if (selectedSeries === 'all' || postSeries === selectedSeries) {
          post.classList.remove('hidden');
        } else {
          post.classList.add('hidden');
        }
      });
    });
  });

  // Tag filtering (only works within currently visible series)
  tagButtons.forEach(button => {
    button.addEventListener('click', function() {
      const selectedTag = this.getAttribute('data-tag');
      
      // Update active button
      tagButtons.forEach(btn => btn.classList.remove('active'));
      this.classList.add('active');
      
      // Filter posts by tag (only within currently visible series)
      postItems.forEach(post => {
        const postTags = post.getAttribute('data-tags').split(' ');
        const isVisible = !post.classList.contains('hidden');
        
        if (selectedTag === 'all') {
          // Show all posts that are currently visible (not hidden by series filter)
          if (isVisible) {
            post.classList.remove('hidden');
          }
        } else {
          // Only filter within currently visible posts
          if (isVisible && postTags.includes(selectedTag)) {
            post.classList.remove('hidden');
          } else {
            post.classList.add('hidden');
          }
        }
      });
    });
  });
});

function toggleFilter() {
  const filterContent = document.getElementById('filterContent');
  const toggleText = document.querySelector('.toggle-text');
  const toggleIcon = document.querySelector('.toggle-icon');
  
  if (filterContent.style.display === 'none') {
    filterContent.style.display = 'block';
    toggleText.textContent = 'Hide Tag Filter';
    toggleIcon.style.transform = 'rotate(180deg)';
  } else {
    filterContent.style.display = 'none';
    toggleText.textContent = 'Show Tag Filter';
    toggleIcon.style.transform = 'rotate(0deg)';
  }
}
</script> 