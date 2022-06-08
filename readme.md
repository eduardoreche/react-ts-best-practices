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
   |- 📁components
       |-📁MyAwesomeComponent
           |-📄index.tsx
           |-📄styles.tsx
   ```
1. Keep component and its styles under a folder named as the component name
1. Keep test files outside of the `src` folder, and also keep them out of your final build

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
