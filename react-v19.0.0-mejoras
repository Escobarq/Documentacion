# Nuevos Hooks en React 19.0.0

## El hook `use`

El hook `use` es una de las adiciones más importantes en React 19.0.0. Este hook funciona como una forma universal de consumir cualquier valor asíncrono o reactivo directamente dentro del cuerpo del componente.

```jsx
function ProfilePage({ userId }) {
  // Puedes usar "use" directamente en el cuerpo del componente
  const user = use(fetchUser(userId));
  
  return <h1>{user.name}</h1>;
}
```

El hook `use` reemplaza muchos casos de `useEffect` porque:
- Puede manejar promesas directamente sin necesidad de estados adicionales
- No requiere arrays de dependencias
- Maneja automáticamente limpieza y cancelación
- Funciona tanto con promesas como con contextos

Anteriormente necesitabas:

```jsx
function ProfilePage({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    let isMounted = true;
    setLoading(true);
    fetchUser(userId)
      .then(data => {
        if (isMounted) setUser(data);
      })
      .catch(err => {
        if (isMounted) setError(err);
      })
      .finally(() => {
        if (isMounted) setLoading(false);
      });
    return () => { isMounted = false; };
  }, [userId]);
  
  if (loading) return <Spinner />;
  if (error) return <ErrorMessage error={error} />;
  return <h1>{user.name}</h1>;
}
```

## API simplificada para `useState`

React 19.0.0 introdujo una sintaxis más concisa para `useState`:

```jsx
// Antes
const [count, setCount] = useState(0);
setCount(count + 1);

// En React 19.0.0
const count = useState(0);
count.set(count.value + 1);
// O incluso: count.update(value => value + 1);
```

Esta nueva sintaxis reduce el boilerplate y es más intuitiva, ya que trabajas con un único objeto que contiene tanto el valor como los métodos para modificarlo.

## Mejoras en `useTransition`

El hook `useTransition` recibió importantes mejoras:

- Mayor rendimiento para transiciones complejas
- API más simple para definir prioridades de renderizado
- Mejor integración con animaciones CSS
- Nuevo sistema de colas para manejar múltiples transiciones

```jsx
function App() {
  const [isPending, startTransition] = useTransition({
    // Nuevas opciones de configuración
    timeout: 3000,  // Tiempo máximo de espera
    priority: 'user-interaction'  // Nueva opción de prioridad
  });

  function handleClick() {
    startTransition(() => {
      // Actualización de baja prioridad
      setPage('dashboard');
    });
  }
}
```

## El nuevo hook `useFormStatus`

Este es un hook completamente nuevo diseñado específicamente para manejar estados de formularios:

```jsx
function SubmitButton() {
  const { pending, data, errors, submitted } = useFormStatus();
  
  return (
    <button type="submit" disabled={pending}>
      {pending ? 'Enviando...' : 'Enviar'}
      {errors && <ErrorMessage errors={errors} />}
    </button>
  );
}

function MyForm() {
  return (
    <form action="/api/submit">
      <input name="email" />
      <SubmitButton />
    </form>
  );
}
```

`useFormStatus` proporciona:
- Estados del formulario (`pending`, `submitted`, `idle`)
- Acceso a los datos actuales del formulario
- Manejo de errores integrado
- Validación automática
- Integración con Server Actions
