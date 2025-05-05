# Vite of the Three Kingdoms  
**A Module Federation Demo for 91life Engineering Challenge**  

![Demo Preview](./path/to/screenshot.png) *Replace with actual screenshot*

## Features  
- ✅ **Host Application** (`apps/host`): Serves as the main shell  
- ✅ **Remote Applications**:  
  - Auroria (`apps/auroria`)  
  - Borealis (`apps/borealis`)  
  - Cygnus (`apps/cygnus`)  
- ✅ **Shared Dependencies**: React & ReactDOM as singletons  
- ✅ **Dynamic Loading**: Host imports components from all remotes  

## Getting Started  

### Prerequisites  
- Node.js ≥18.x  
- pnpm ≥9.x  

### Installation  
```bash  
pnpm install  
```

### Running the Apps  
```bash  
# Host (Port 4200)  
pnpm nx serve host  

# Remotes (Run in separate terminals)  
pnpm nx serve auroria --port=4201  
pnpm nx serve borealis --port=4202  
pnpm nx serve cygnus --port=4203  
```

Access the host at: http://localhost:4200  

## Technical Approach  

### Key Implementations  
1. **Vite Configuration**  
   - Manual setup of `vite.config.ts` for each app  
   - Module Federation configured with:  
     ```ts  
     shared: ['react', 'react-dom'] // Ensures singleton instances  
     ```  

2. **Cross-App Communication**  
   - Host dynamically imports components:  
     ```tsx  
     const RemoteComponent = React.lazy(() => import('remote-app/Component'));  
     ```  

### Challenges & Solutions  
- **Nx Plugin Integration**:  
  Developed a custom generator (`@91life/nx-mf-vite`) to automate configurations.  
  *Final hurdle*: Generator registration issues in Nx 20.8.1 (see [Technical Notes](#technical-notes)).  

- **Dependency Management**:  
  Enforced version alignment across all apps through manual `package.json` checks.  

## Project Structure  
```  
apps/  
├── host/           # Host application  
├── auroria/        # Remote app 1  
├── borealis/       # Remote app 2  
└── cygnus/         # Remote app 3  

packages/  
└── nx-mf-vite/     # Custom plugin (WIP - see notes)  
```

## Technical Notes  
- **Generator Challenge**:  
  The `@91life/nx-mf-vite` plugin successfully:  
  - Scaffolds Module Federation configuration  
  - Manages shared dependencies  
  - *Current Limitation*: Final integration with Nx's generator API requires additional debugging  

- **Workaround Implemented**:  
  Manual configuration was used to ensure fully functional submission while resolving:  
  ```bash  
  # Initial generator attempt  
  nx g @91life/nx-mf-vite:setup-vite-mf --project=host --type=host  
  ```  

## Future Improvements  
1. Complete Nx plugin integration  
2. Add shared UI component library  
3. Implement CI/CD pipeline with automated testing  

## Acknowledgments  
- **Vite** for blazing-fast tooling  
- **Module Federation** pattern for microfrontend architecture  
- **Nx** for monorepo management  

---

**Contact**: kjashar31@gmail.com | [LinkedIn Profile](https://www.linkedin.com/in/korabjashari/)
