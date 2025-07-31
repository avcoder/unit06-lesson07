---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /assets/intro.jpg
# some information about your slides (markdown enabled)
title: Software Development | Foundations
info: |
  ## Software Development | Foundations
# apply unocss classes to the current slide
class: text-left
drawings:
  persist: false
transition: slide-left
mdc: true
---

# React Router
Frontend Development: Unit 06 - Lesson 07

- [ ] BrowserRouter, Routes, Route, Link
- [ ] useContext
- [ ] useReducer

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
-->


---
transition: slide-left
---

# Recap
- Q: In traditional server-side websites what happens when you goto `/posts` or `/users/:userId`?  
   - Q: Is there a direct correlation between path and actual physical folder org?
- Server-side routing is usually slower as page reloads as indicated by the brief white flicker as page reloads
- Here's how to do a basic URL Change without a reload:
  ```js
  // goto amazon.ca
  history.pushState({ page: 1 }, '', '/deals'); // console.log(location.pathname)
  ```
  - Then try `history.back()` and `history.forward()
- Recall that AJAX allows parts of a page to reload without full page refresh (think google maps)

---
transition: slide-left
---

# Client-Side Routing using React Router

1. User clicks a `<Link to="/about">` component
   - unlike a regular anchor tag, React Router's `<Link>` prevents a full page reload
2. The click event is intercepted and `event.preventDefault()` stops the browser from actually navigating to `/about` and reloading the page
3. React Router updates the browser's address bar (it uses history.pushState())
4. React Router tries to match the new route with the component you want displayed
5. React renders the component you want displayed via `<Route path="/about" element={<About />}`
6. Browser history is preserved so that back/forward navigation is still functional

---
transition: slide-left
---

# Advantages for Client-Side Routing

```jsx
// in main.jsx/tsx
<BrowserRouter>
  <Routes>
      <Route path="/about" element={<About />} />
  </Routes>
</BrowserRouter>

// in App.jsx/tsx
<nav>
  <Link to="/about">About</Link/>
</nav>
```

- Faster Navigation: no more flash of white nothingness on page reload but rather is instant
- Better UX: smoother transitions, more App-like Behaviour (SPA), React state is preserved
- Reduced Server Load: Server now primarily serves JSON via API requests
- Routes map directly to React components making routing logic highly composable and maintainable
- Provides: Nested Routing (`/recipes/chicken`), and dynamic routing (`/recipes/:id`)
- Handles edge cases related to `history.pushState` and `history.back/forward`

---
transition: slide-left
---

# Install React Router

- `npm i react-router`
- in `main.tsx`:
  ```jsx
  import { BrowserRouter } from "react-router";
  // inside root.render > <StrictMode>
  <BrowserRouter>
    <App />
  </BrowserRouter>
  ```
- 🤔 Now examine React dev tools > Components


---
transition: slide-left
---

# Basic Routing
Refactor App.tsx such that our nav displays and navigates to every Lesson we've done so far

- in `App.tsx`:
  ```jsx
  import { Routes, Route, Link } from "react-router";
  // inside return (
    <>
      <nav className="nav">
        <Link to="lesson01">Lesson 01</Link>
        <Link to="lesson02">Lesson 02</Link>
      </nav>
      <Routes>
        <Route path="lesson01" element={<Lesson01 />} />
        <Route path="lesson02" element={<Lesson02 />} />
      </Routes>
  ```
- Optional: in App.css, use `.nav` to style: `<nav className='nav'`
  ```css
  .nav {
    display: flex;
    gap: 10px;
    justify-content: center;
    list-style-type: none;
    flex-wrap: wrap;
  }
  ```
- Does navigation still work even if you click the "Back" and "Forward" button?

---
transition: slide-left
---

# Exercise: Basic Routing

- Refactor https://github.com/avcoder/email-react-template to do Basic Routing
- import BrowserRouter, Routes, Route, Link as needed
- Make the sidebar "Calendar", route to `<Calendar />` such that it replaces the Inbox and the EmailBody areas of the page
- Same with "Notes"
- Same with "Contacts"
- Make clicking Inbox go back to original view
- Under dev tools > Network tab > verify there is no GET/POST request when re-routing to different components

---
transition: slide-left
---

# Routes vs Layouts
- Good practice to:
  - place routes in AppRouter.tsx for future ease of maintainability
  - decouple layout concerns separated from routing for future scalability and flexibility
  - Optional can use `<NavLink>` for additional styling considerations
  ```jsx
  // in AppRouter.tsx
  return (
    <Layout>
      <Routes>
        ...
      </Routes>
    </Layout>
  )
  ```
  ```jsx
  const Layout: React.FC<LayoutProps> = ({ children }) => { // in Layout.tsx
  return (
    <>
      <Header />
        {children}
      <Footer />
    </>
  )
  ```

---
transition: slide-left
---

# Nested Routes

---
layout: image-right
transition: slide-left
image: /assets/tyler.png
backgroundSize: 420px 400px
class: text-left
---

# 10 minute break

🍦 Cool Tips, Trends and Resources:

- 🚦 [Build your own React Router](https://ui.dev/build-your-own-react-router)
- 🔊 [Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
- 🤔 [Thinking in React](https://react.dev/learn/thinking-in-react)
- 🍬 [Github Student Dev Pack](https://education.github.com/pack)

<br>
<hr>
<br>

- 🧪 [Enter anonymous lab questions](https://docs.google.com/forms/d/e/1FAIpQLSevvGARdHQikso-uLqFCO481MABKE5HofuSrlzEPMNQ2ZLykw/viewform?usp=dialog)
- ℹ️ [Course feedback survey](https://circuitstream.typeform.com/to/ZoyYk7px#course_id=SoftwareAN&instructor=9514)

---
transition: slide-left
---

# useContext
see https://react.dev/reference/react/useContext

---
transition: slide-left
---

# useReducer
see https://react.dev/reference/react/useReducer

---
transition: slide-left
---

# Homework

- Refactor the weather app we did for our first exercise (see https://codepen.io/codevilla/pen/YPyWWpm) into the following components.  Then separate the css into its respective components that you created.
Feel free to create more components inside `<Forecast>` as you see fit.  FYI - ignore my `this.whatever` or `this.state.whatever` code below since I was using class-based React which you won't be using.
  ```jsx
  return (
      <div>
        <header>
          <Nav city={this.state.currentCity} handleCityChange={this.changeCity} />
        </header>
        <main>
          <TodayWeather
            city={this.state.currentCity}
            handleCoordsChange={this.changeCoords}
          />
          <Forecast lat={this.state.lat} lon={this.state.lon} />
        </main>
      </div>
    );
  ```
- Start working on "Weather Forecasting App" assignment due Aug 17 midnight EST
