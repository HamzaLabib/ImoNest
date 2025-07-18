# EmoNest App Devlog

## Week 1
**Update:**  
- Brainstormed the core idea of the app — a safe emotional expression space for children. Outlined initial features, user flows, and the emotional tone the app should evoke.
- Evaluated key technologies (React Native, Expo, Expo Router, AsyncStorage, tsx vs jsx), and made deliberate decisions around simplicity and scalability.
- Designed the app structure on paper and mentally mapped how children would interact with the app — considering empathy, safety, and engagement.
- Planned the multi-page layout, navigation logic, and future scalability for adding adult features.
- Established the MVP scope to prioritize what was truly essential for launch.

**Challenges:**  
- Defining a simple, realistic MVP that still conveyed the emotional intent of the app without falling into feature creep.
- Choosing the right combination of tools and architectural approach early on to avoid major rewrites later.

**Key Learnings:**  
- Learned the importance of investing time in upfront design and planning before touching code.
- Gained clarity on the relationship between app intent (emotional safety) and UX design decisions (color, layout, onboarding flow).

---

## Week 2
**Update:**  
- Designed a scalable folder structure for the frontend including `screens`, `components`, `utils`, `scripts`, `assets`, and `services`.
- Gathered and organized visual resources like images, mood emojis, and animated clips.
- Chose consistent UI patterns for both child and parent experiences and began building reusable components (e.g., `CustomInput`, `MoodButton`, `MessageBubble`).
- Started implementing the UI one screen at a time, frequently pausing to test and refactor for consistency.
- Prioritized accessibility and emotional clarity in visual elements (e.g., large tap targets, playful text, soft visuals).

**Challenges:**  
- Deciding on how to balance design simplicity with features like animated mood feedback, audio input, and chat responses.
- Managing navigation and conditional rendering based on authentication without losing UX flow.

**Key Learnings:**  
- Learned to apply mobile-first UX principles, especially for children, where simplicity and clarity are critical.
- Understood the value of designing with emotion in mind — every icon, word, and transition had to contribute to a sense of safety and fun.

---

## Week 3
**Update:**  
- Finished major frontend screens including mood selection, chatbot interaction, microphone functionality, and drawing placeholders.
- Conducted iterative design-refactor cycles to improve layout, spacing, and responsiveness across devices.
- Wrapped up frontend phase by cleaning unused components and ensuring smooth transitions.
- Started backend development: implemented simple login/signup API using Node.js and tokens.
- Chose MongoDB as the database for its document flexibility and ease of integration with Express.
- Integrated backend with frontend and tested authentication flow.

**Challenges:**  
- UI/UX responsiveness across screen sizes and dynamic keyboard issues (`KeyboardAvoidingView`).
- Linking frontend to backend and updating authenticated screens without forcing a full app reload — required a deep dive into routing logic and async state handling.
- Debugging took two days of testing endpoints, navigation state, and rethinking layout structure.

**Key Learnings:**  
- Learned to architect navigation with reactivity in mind — not just static routes.
- Understood the critical importance of modularizing authentication logic for dynamic updates and reusability.

---

## Week 4 (Deployment Phase – The Last 3 Days)

**Update:**  
- Transitioned from development to deployment, targeting **expo publish**, **Netlify** and **Vercel** for hosting the web version of the Expo app.  
- Faced no longer supports recent Node.js versions, multiple 404 errors on Netlify due to missing SPA routing configuration. Researched and implemented `_redirects` file with `/* /index.html 200` to handle Expo Router navigation correctly.  
- Learned that the `dist/` folder is regenerated by `expo export`, which deletes manual files. Solved this by creating a custom `postexport:web` script in `package.json` to automatically copy the `_redirects` file into the build folder after export but I failed.  
- Switched to Vercel for testing — configured `vercel.json` with `@vercel/static-build`, added a `vercel-build` script, and set the output directory to `dist` and I copied it.  
- Encountered blank screens on deploy. Diagnosed the problem as a result of trying to use `Alert.alert()` and `expo-file-system`, which don’t work well in browser environments.  
- Rewrote platform-specific logic in `storageUtils.js` to use `localStorage` on web instead of file system storage, solving mood history display issues.  
- Replaced unsupported `Alert.alert()` on web with `window.prompt()` fallback, ensuring the activity selection feature works reliably across platforms.  
- Added cross-platform `logout` support using a global auth context and dynamic route handling via Expo Router.  
- Finalized layout and screen enhancements, including a persistent logout button, working cross-platform authentication, and secure mood logging.  

**Challenges:**  
- Navigating platform-specific limitations between mobile and web (e.g., file storage APIs, alerts, routing).  
- Ensuring consistency between build artifacts and what gets served in static deployment environments like Vercel and Netlify.
- Diagnosing silent runtime failures in deployed apps where tools like `Alert` or `FileSystem` silently fail on web.
- Repeating export-redeploy cycles and tracking changes across build tools and hosting platforms — a surprisingly time-consuming loop.

**Key Learnings:**  
- Learned the deep difference between mobile-native APIs and browser limitations — and how to create fallbacks (`localStorage`, `window.prompt`) that maintain functionality.  
- Gained insight into CI/deployment automation with `postexport` and custom scripts for Expo + web.  
- Understood the value of platform-aware logic using `Platform.OS` to ensure code behaves properly across environments.  
- Realized how crucial clear build configuration (`vercel.json`, `netlify.toml`, `_redirects`) is when dealing with static SPA routing.  
- Developed patience and sharper debugging skills while resolving non-obvious deploy-time bugs.

---

## Additional Challenges
- Simplifying ambitious ideas into practical, iterative tasks
- Creating consistent and clean reusable logic across components
- Managing local state and `AsyncStorage` tokens in a responsive and secure way
- Refactoring navigation state to support dynamic layout re-evaluation post-login
- Balancing time between code quality, app polish, and final delivery goals

---

**Reflection:**  
This project helped me grow as a full-stack mobile developer — from brainstorming and designing an emotionally thoughtful product to executing each phase with flexibility and care. The deliberate focus on planning, folder architecture, UX design, and component structure made development smoother. Every bug, layout issue, and integration hurdle sharpened my debugging and problem-solving skills. Most importantly, I learned how to think from both a child user's perspective and a developer’s mindset — blending empathy with logic.
