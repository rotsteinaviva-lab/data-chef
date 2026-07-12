---
layout: home
title: "Data Chef Blog Home"
---
<!-- Main Parent Container: Sets up the two-column grid layout -->
<div style="display: grid; grid-template-columns: 250px 1fr; gap: 40px; margin: 20px auto; max-width: 1200px; font-family: sans-serif;">

  <!-- Left Column: The Tag Sidebar -->
  <aside style="align-self: start; background: #f9f9f9; padding: 20px; border-radius: 8px; border: 1px solid #e0e0e0;">
    <h3 style="margin-top: 0; color: #333;">Filter by Tag</h3>
    <div style="display: flex; flex-direction: column; gap: 10px;">
      <a href="/tags/java" style="text-decoration: none; color: #007acc; padding: 6px 12px; background: #fff; border: 1px solid #ddd; border-radius: 4px; font-size: 14px;"># java (5)</a>
      <a href="/tags/markdown" style="text-decoration: none; color: #007acc; padding: 6px 12px; background: #fff; border: 1px solid #ddd; border-radius: 4px; font-size: 14px;"># markdown (3)</a>
      <a href="/tags/webdev" style="text-decoration: none; color: #007acc; padding: 6px 12px; background: #fff; border: 1px solid #ddd; border-radius: 4px; font-size: 14px;"># webdev (12)</a>
    </div>
  </aside>

  <!-- Right Column: Standard Blog Feed -->
  <section>
    <h2 style="margin-top: 0; border-bottom: 2px solid #eaecef; padding-bottom: 8px;">Recent Blog Posts</h2>
    
    <div style="margin-bottom: 30px;">
      <h3 style="margin-bottom: 5px;"><a href="/blog/first-post" style="color: #24292e; text-decoration: none;">How to Build a Modern Blog Sidebar</a></h3>
      <small style="color: #586069;">Published: July 11, 2026</small>
      <p style="color: #24292e; line-height: 1.5;">This guide walks you through building complex side-by-side elements without abandoning your favorite Markdown ecosystem.</p>
    </div>

    <div style="margin-bottom: 30px;">
      <h3 style="margin-bottom: 5px;"><a href="/blog/java-tips" style="color: #24292e; text-decoration: none;">Mastering Java Front-Matter Metadata</a></h3>
      <small style="color: #586069;">Published: July 10, 2026</small>
      <p style="color: #24292e; line-height: 1.5;">Learn how compilation engines extract arrays from Markdown front-matter fields to build structured navigation menus seamlessly.</p>
    </div>
  </section>

</div>
