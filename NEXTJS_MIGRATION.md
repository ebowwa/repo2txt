# Next.js Migration Plan for Repo2Txt

## Overview

This document outlines the plan to migrate the current static HTML/JavaScript application to a modern Next.js client-side application. The migration will maintain the current browser-only processing while adding modern features and improved user experience.

## Architecture

### Technology Stack

- **Framework**: Next.js 14+ (App Router)
- **Styling**: Tailwind CSS
- **State Management**: React Context + Hooks
- **File Processing**: Browser File API + JSZip
- **UI Components**: Shadcn/ui
- **Code Highlighting**: Prism.js or Shiki
- **Icons**: Lucide React

### Key Features to Implement

1. **Client-Side Only Processing**
   - Use `'use client'` directives
   - Implement file processing in browser
   - Maintain zero server dependency

2. **Modern UI Components**
   ```tsx
   // Example component structure
   components/
   ├── ui/
   │   ├── Button.tsx
   │   ├── FileTree.tsx
   │   └── CodePreview.tsx
   ├── features/
   │   ├── GithubRepo/
   │   └── LocalDir/
   └── layouts/
   ```

3. **Routing Structure**
   ```
   app/
   ├── page.tsx              # GitHub repo converter
   ├── local/
   │   └── page.tsx         # Local directory converter
   └── layout.tsx           # Common layout
   ```

## Implementation Steps

1. **Project Setup**
   ```bash
   npx create-next-app@latest repo2txt-next
   cd repo2txt-next
   npm install @shadcn/ui jszip prismjs lucide-react
   ```

2. **Core Features Migration**
   - Convert existing JavaScript modules to TypeScript
   - Implement React components for UI elements
   - Add file processing hooks
   - Setup state management

3. **UI/UX Improvements**
   - Dark mode support
   - Responsive design
   - Loading states
   - Error handling
   - Progress indicators

4. **New Features**
   - Live preview
   - Multiple export formats
   - Customizable templates
   - File search and filtering
   - Batch processing

## Code Examples

### File Processing Hook
```typescript
const useFileProcessor = () => {
  const [files, setFiles] = useState<File[]>([]);
  const [processing, setProcessing] = useState(false);
  
  const processFiles = async (input: FileList) => {
    setProcessing(true);
    try {
      // File processing logic
    } catch (error) {
      console.error(error);
    } finally {
      setProcessing(false);
    }
  };

  return { files, processing, processFiles };
};
```

### GitHub Repository Component
```typescript
'use client'

export default function GithubRepo() {
  const [repoUrl, setRepoUrl] = useState('');
  const { processRepo, loading } = useGithubRepo();

  return (
    <div className="container mx-auto p-4">
      <input 
        type="text"
        value={repoUrl}
        onChange={(e) => setRepoUrl(e.target.value)}
        placeholder="Enter GitHub repository URL"
        className="w-full p-2 border rounded"
      />
      <Button 
        onClick={() => processRepo(repoUrl)}
        disabled={loading}
      >
        Process Repository
      </Button>
    </div>
  );
}
```

## Development Guidelines

1. **TypeScript First**
   - Use strict type checking
   - Create interfaces for all data structures
   - Implement proper error handling

2. **Performance**
   - Use React.memo for heavy components
   - Implement virtual scrolling for large file lists
   - Optimize file processing with Web Workers

3. **Testing**
   - Unit tests with Jest
   - Component tests with React Testing Library
   - E2E tests with Playwright

4. **Accessibility**
   - ARIA labels
   - Keyboard navigation
   - Screen reader support

## Deployment

1. **Static Export**
   ```bash
   npm run build
   npm run export
   ```

2. **Hosting Options**
   - Vercel (recommended)
   - GitHub Pages
   - Netlify
   - Cloudflare Pages

## Timeline

1. **Week 1**: Project setup and core component migration
2. **Week 2**: File processing implementation
3. **Week 3**: UI/UX improvements
4. **Week 4**: Testing and deployment

## Getting Started

```bash
# Clone the repository
git clone [repo-url]
cd repo2txt-next

# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build
```

Visit `http://localhost:3000` to see the application in development mode.
