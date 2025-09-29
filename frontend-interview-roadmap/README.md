# Frontend Interview Roadmap - Contribution Guidelines

This `README.md` outlines the instructions and best practices for contributing to the Frontend Interview Roadmap. Our goal is to create a comprehensive, clear, and highly valuable resource for frontend developers preparing for interviews.

## 📝 Structure of a Question File

Each question should have its own Markdown file (`.md`) within the appropriate topic directory (e.g., `javascript/`, `react/`, `nextjs/`, `css-styling-ux/`, `docker-devops/`).

Every question file **must** follow this structure:

```markdown
# [Question Number]. [Question Title]

## Quick Revision

[A concise, 2-3 sentence summary of the answer. Ideal for quick recall.]

## Detailed Explanation

[A thorough, in-depth explanation of the concept. This should cover the "why" and "how", discuss nuances, pros/cons, and related concepts. Aim for clarity and comprehensive understanding.]

### Key Concepts (Optional, but recommended for complex topics)

[List and briefly explain any core terms or ideas relevant to the question.]

## Code Examples

[Provide practical, runnable code examples that illustrate the concept. Code should be well-commented and easy to understand. Include both good and bad examples where appropriate to highlight best practices or common pitfalls.]

## Do's and Don'ts (Optional, but recommended)

### Do

*   [Action 1]
*   [Action 2]

### Don't

*   [Action 1]
*   [Action 2]

## Resources

[A curated list of external resources for further learning. **Crucially, all URLs must be working and relevant.** Include a mix of official documentation, reputable articles, and high-quality video tutorials/courses. Aim for at least 3-5 resources per question.]

*   **Article:** [Title of Article](https://example.com/article-link)
*   **Official Docs:** [Title of Documentation](https://example.com/docs-link)
*   **Video:** [Title of Video](https://www.youtube.com/watch?v=video-link)
*   **Course:** [Title of Course](https://example.com/course-link)
```

## ✍️ Guidelines for Content

1.  **Clarity and Conciseness:** Explain complex topics in simple, easy-to-understand language. Avoid jargon where possible, or explain it clearly.
2.  **Depth:** Go beyond surface-level definitions. Explain the underlying mechanisms, trade-offs, and real-world implications of each concept.
3.  **Code Examples:** Provide clear, runnable, and practical code examples. Use appropriate syntax highlighting. Explain *why* the code works the way it does.
4.  **References:** **Verify all URLs.** Ensure they are active, point to the correct content, and are from authoritative sources (official documentation, well-regarded blogs, educational platforms). Include a variety of formats (articles, videos, courses) if available.
5.  **Difficulty Levels:** Feel free to add questions that span from intermediate to advanced levels. Clearly indicate the expected difficulty if it's not obvious from the question title.
6.  **No Vue.js Specific Questions:** As per the initial instruction, please **ignore** any questions that are specifically about Vue.js. This roadmap focuses on general frontend, React, Next.js, CSS/UX, and Docker/DevOps.
7.  **Originality:** While referencing external resources is encouraged, ensure your explanations are original and not simply copied verbatim.

## 📁 Naming Convention

*   **Directory Names:** Use kebab-case (e.g., `css-styling-ux`, `docker-devops`).
*   **File Names:** Use a numerical prefix followed by kebab-case for the question title (e.g., `1-what-is-docker.md`, `15-accessibility.md`). This helps maintain order and makes linking easier.

## 🔗 Updating the Main Roadmap File

After adding a new question file, you **must** update the main `frontend-interview-roadmap.md` file to include a link to your new question. Maintain the numerical order within each section.

```markdown
## 🐳 Docker & DevOps (Frontend Context)

- [1. What is Docker?.](./docker-devops/1-what-is-docker.md)
- [2. Containers vs VMs.](./docker-devops/2-containers-vs-vms.md)
- [New Question Title.](./docker-devops/XX-new-question-file.md)
```

By following these guidelines, we can build a high-quality and consistent resource for the frontend community. Thank you for your contributions!