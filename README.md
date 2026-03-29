Actividad 4: Troubleshooting
Snippet 1 corregido
name: CI Pipeline

on:
  push:
    branches: [main]
  pull_request:
    branches: [main, develop]

jobs:
  test:
    runs-on: ubuntu-latest

Snippet 2 corregido
deploy:
  runs-on: ubuntu-latest
  environment: production
  steps:
    - uses: actions/checkout@v4
    - name: Deploy to Vercel
      run: vercel --prod --token $VERCEL_TOKEN
      env:
        VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
Snippet 3 corregido
test:
  runs-on: ubuntu-latest
  strategy:
    matrix:
      node-version: [18.x, 20.x]
  steps:
    - uses: actions/checkout@v4
    - uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    - run: npm ci
    - run: npm test

Actividad 5: Preguntas Conceptuales
1. Diferencia entre CI y CD
La Integración Continua (CI) permite integrar cambios de código frecuentemente con pruebas automáticas. La Entrega Continua (CD) permite que el software esté listo para desplegarse automáticamente.

2. Qué es un self-hosted runner
Es un servidor propio que ejecuta workflows de GitHub Actions en lugar de usar los de GitHub. Se utiliza cuando se requiere más control o recursos.

3. Propósito de GitHub environments
Permiten gestionar entornos como producción o desarrollo, controlar despliegues y manejar secrets específicos.

4. Qué es una rollback strategy
Es una estrategia para regresar a una versión anterior si un deployment falla, asegurando estabilidad del sistema.