# React Typescript Best Practices

## Components

### Definition

1. Prefer simple functions to declare components
2. Export not as default at the end of the file
3. Keep all your states declared first in your component function
4. `useEffect`'s should be declared first, before other internal methods
5. Prefer `interfaces` over `types`
6. Destructure props

   ```typescript
   interface IProps {
       color: string;
       maxWidth?: number;
   }

   function MyComponent({color, maxWidth? = 100}: IProps) {
       const [myState, setMyState] = useState(0);

       useEffect(() => {}, []);

       const handleSomething = () => {}

       return ();
   }

   export { MyComponent }
   ```

### Naming convention and folder structure

1. Folder structure
   ```
   📁__tests__
     |-📁components
     |-📁contexts
     |-📁hooks
   📁src
   |-📁components
        |-📁MyAwesomeComponent
            |-📄index.tsx
            |-📄styles.tsx
   |-📁containers
       |-📁IncredibleContainer
           |-📄index.tsx
           |-📄styles.tsx
       |-📁ComplexContainer
           |-📁ComplexPieceContainer              
              |-📄index.tsx
              |-📄styles.tsx              
           |-📁ComplexPartContainer              
              |-📄index.tsx           
           |-📄index.tsx
   |- 📁contexts
        |-📃auth.tsx
        |-📃otherContext.tsx
   |- 📁hooks
        |-📃format.ts
   |- 📁pages
        |-📃Home.tsx     
        |-📃UserProfile.tsx     
   |- 📁services
        |-📁api
            |-📃apiClient.ts
            |-📃queryClient.ts
        |-📃routes.ts  
   |- 📁store
        |-📃index.ts     
        |-📃userSlice.ts
   |- 📁styles
        |-📃global.css
        |-📃theme.tsx
   ```
1. Keep component and its styles under a folder named as the component name
1. Keep test files outside of the `src` folder, and also keep them out of your final build
1. If needed, split your containers in smaller ones, keeping one index file that put it together.
2. Use <a href="https://bradfrost.com/blog/post/atomic-web-design" target="_blank">Atomic Design 🔗</a> to organize and decide about pages, containers, components and more.

### Import declarations

1. Order your imports by importance (react always first, then other external libs, then your app items...)
1. Keep subjects close, as giving space between groups

   ```typescript
   import { useEffect, useState } from 'react';
   import { Box } from 'material-ui';
   import { useNavigate } from 'react-router-dom';

   import { MyComponent } from '../components/MyComponent';
   import { MyOtherCmp } from '../components/MyOtherCmp';

   import { useAwesome } from '../hooks/awesome';
   import { useGreeting } from '../hooks/greeting';

   import { MyContextProvider, useMyContext } from '../contexts/myContext';

   import { Container, Shadow } from './styles';
   ```
   
### Context API
  
   #### Code Context API as a PRO!

```typescript
const MyContext = createContext<MyContextData>({} as MyContextData);

export const MyContextProvider = ({children}: IProps) => {

   const fetchData = () => {...}

   const contextValue = useMemo(() => ({
      data,
      fetchData
   }), [data]);

   return <MyContext.Provider value={contextValue}>{children}</MyContext.Provider>
}

export const useMyContext = () => {
   const context = useContext(MyContext);

   if(!context) throw new Error('useMyContext must be used within a MyContextProvider');

   return context;
}
```

   #### ...and use it as SENIOR dev

```typescript
   //MyContainer.tsx
   export const MyContainer () => {
      ... 
      return (
         <MyContextProvider>
            <MyComponent />
            <AnotherComponent />
         </MyContextProvider>
      )
   }

   //MyComponent.tsx
   export cont MyComponent () => {
      const [data, fetchData] = useMyContext();

      ...

      return (
         <div>{data}</div>
      )
   }
```
