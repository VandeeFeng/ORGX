# 🚧 ORGX is currently cooking! 🍳

# ORGX ✨

**ORGX: Bringing the power of JSX components directly into your Org Mode documents.**

Inspired by [MDX](https://mdxjs.com/), ORGX allows you to seamlessly embed JSX components (like React or Vue components) within your Org Mode files, enabling you to build rich, interactive content and documentation websites with the power of Org's structure and the flexibility of modern component frameworks.

## 🤔 Why ORGX?

Org Mode is an exceptional tool for outlining, note-taking, and authoring structured documents. Modern web development heavily relies on component-based architectures (React, Vue, Svelte, etc.) for building UIs.

While Org Mode's built-in export (`org-export`) is powerful for generating static formats like HTML, integrating complex, interactive JavaScript components directly within the Org workflow in a truly seamless way can be challenging.

MDX successfully bridged this gap for Markdown. **ORGX aims to do the same for Org Mode.**

ORGX allows you to leverage Org's fantastic writing experience while directly embedding and utilizing your existing frontend components, creating a unified workflow for content and application logic.

## 🚀 Core Features

- **JSX in Org:**

  Write JSX syntax directly inside your `.org` files.

  ```
  * My Interactive Section
  <MyChart data={myData} />
  ```

- **Component Imports:**

  Import your components, typically within a designated setup block or frontmatter (exact mechanism TBD).

  ```
  #+BEGIN_SETUP
  import { MyChart } from './components/MyChart.jsx'
  const myData = [10, 20, 15, 30];
  #+END_SETUP
  
  * Chart Example
  Here's the chart: <MyChart data={myData} title="Sample Data" />
  ```

- **Org Syntax Compatibility:** Continue using familiar Org Mode syntax like headlines, lists, links, emphasis, tables, etc. ORGX aims to parse and convert standard Org structures alongside your JSX.

- **Compilation to Components:** ORGX processes your `.org` files and compiles them into standard JavaScript components (e.g., React functional components) that can be used within your frontend application.

- **Build Tool Integration:** Designed to integrate with modern JavaScript build tools like Vite, Webpack, Next.js, etc., through dedicated loaders or plugins (similar to how MDX is integrated).

## ⚙️ How it Works (Conceptual)

1. **Parsing:** ORGX parses your `.org` file, understanding both standard Org Mode syntax and the embedded JSX elements, imports, and JavaScript expressions. This likely involves extending an existing Org parser (like `orgajs`) or using a custom parser.

2. **AST Transformation:**

   It creates an Abstract Syntax Tree (AST) representing the combined structure. This AST is then transformed:

   - Org elements (headlines, paragraphs, lists) are converted into corresponding JSX elements (e.g., `<h1>`, `<p>`, `<ul>`).
   - JSX elements, imports, and expressions from your file are preserved and integrated into the structure.

3. **Compilation:** The transformed AST is compiled into a runnable JavaScript component (e.g., a React component exporting a function).

4. **Integration:** Your build tool uses the ORGX loader/plugin to handle `.org` files, allowing you to `import MyOrgPage from './my-page.org'` just like any other component.

## 📦 Installation (Planned)

```
# Using npm
npm install orgx --save-dev

# Using yarn
yarn add orgx --dev
```

*(Note: ORGX is currently under development. Installation instructions are provisional.)*

You will also need to configure your build tool (Vite, Webpack, Next.js, etc.) to use the ORGX plugin/loader. Documentation for specific integrations will be provided later.



## 📝 Example Usage

Imagine a file named `src/pages/hello.org`:

```
#+TITLE: My ORGX Page
#+SETUP:
import { useState } from 'react';
import { Button } from '../components/Button.jsx';
import { Alert } from '../components/Alert.jsx';
const initialCount = 0;
#+END_SETUP

* Welcome to ORGX!

This page demonstrates embedding interactive React components within an Org Mode file.

Here's a standard Org list:
- Item 1
- Item 2

** An Interactive Counter **

Let's add a counter component:

#+BEGIN_SRC jsx
{() => {
  const [count, setCount] = useState(initialCount);
  return (
    <div>
      <p>Current count: {count}</p>
      <Button onClick={() => setCount(count + 1)}>Increment</Button>
    </div>
  );
}}
#+END_SRC

You can mix Org text around your components freely.

Here's another component:
<Alert type="info" message="This is an Alert component!" />

Standard Org formatting like *bold* and /italic/ still works.
```

When processed by ORGX and your build tool, importing `hello.org` in your React application would render a page containing the formatted Org text and the interactive `Button` and `Alert` components.

*(Note: The exact syntax for imports (`#+SETUP`) and embedding complex logic (`#+BEGIN_SRC jsx ...`) is preliminary and subject to change based on implementation details.)*
