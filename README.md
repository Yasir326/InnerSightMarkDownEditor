# InnerSight Inline Markdown Editor

A Bear‑style inline Markdown editor for React Native (iOS + Android). It renders styled markdown **as you type**, keeps plain text markdown as the source of truth, and supports incremental parsing for speed.

---

## ✨ Features

* **Inline formatting**: bold, italic, headings, inline code, code blocks, blockquotes
* **Tasks**: interactive checkboxes that toggle with a tap
* **Links**: tap to open links
* **Markers dimmed**: syntax characters (`**`, `#`, etc.) are visually dimmed
* **Incremental parsing**: only re-parses the changed lines for smooth editing
* **Cross‑platform**: iOS (TextKit) and Android (Spannable) native implementations
* **Toolbar**: simple toolbar for bold, italic, heading, task, and code insertion

---

## 📦 Installation

1. Add the package to your project (if published to npm, otherwise clone this repo):

   ```bash
   yarn add react-native-inline-md-editor
   # or
   npm install react-native-inline-md-editor
   ```

2. Link native code:

   * **iOS**: Make sure Swift bridging is enabled, and add `RNMarkdownEditorManager.swift` + `RNMarkdownEditorView.swift` to your target.
   * **Android**: Autolinking should pick it up. If not, add `RNMarkdownEditorPackage()` to your `MainApplication`.

---

## 🚀 Usage

```tsx
import React, { useState } from 'react';
import { SafeAreaView, Linking } from 'react-native';
import { MarkdownEditor } from 'react-native-inline-md-editor';
import { Toolbar } from './Toolbar';

export default function App() {
  const [value, setValue] = useState<string>(
    `# Notes\n\n- [ ] Inline **markdown** with *italic* and \`code\`.\n- [x] Tap the box to toggle.\n\n> Quote\n\n\`\`\`\ncode block\n\`\`\`\n\nLink: [rn docs](https://reactnative.dev)`
  );
  const [selection, setSelection] = useState({ start: 0, end: 0 });

  return (
    <SafeAreaView style={{ flex: 1 }}>
      <Toolbar
        value={value}
        selection={selection}
        setValue={setValue}
        setSelection={setSelection}
      />
      <MarkdownEditor
        value={value}
        selection={selection}
        onChangeText={setValue}
        onSelectionChange={(s, e) => setSelection({ start: s, end: e })}
        onLinkPress={href => Linking.openURL(href)}
        style={{ flex: 1, padding: 12 }}
      />
    </SafeAreaView>
  );
}
```

---

## 🛠 Development

* **Tokenizer**: Implemented in TypeScript, parses only changed lines.
* **Native views**:

  * iOS uses `UITextView` with attributed text.
  * Android uses `AppCompatEditText` with spans.
* **Decorations**: passed from JS → native as ranges with attributes.

---

## 📂 Project structure

```
react-native-inline-md-editor/
├─ package.json
├─ src/
│  ├─ MarkdownEditor.tsx
│  ├─ tokenize.ts
│  ├─ decorations.ts
│  ├─ utils/
│  │  └─ lines.ts
│  └─ index.ts
├─ ios/
│  ├─ RNMarkdownEditorManager.swift
│  ├─ RNMarkdownEditorView.swift
│  └─ RNMarkdownEditorManager.m
├─ android/
│  └─ src/main/java/com/rnmarkdowneditor/
│     ├─ RNMarkdownEditorManager.kt
│     ├─ RNMarkdownEditText.kt
│     └─ RNMarkdownEditorPackage.kt
└─ example/
   ├─ App.tsx
   └─ Toolbar.tsx
```

---

## 📌 Roadmap

* [ ] Hide syntax markers completely (not just dim)
* [ ] Syntax highlighting inside fenced code blocks
* [ ] List indentation with Tab/Shift+Tab
* [ ] Fabric port for RN new architecture

---

## 📜 License

MIT © 2025
