# Convenciones de testing

> Cómo escribimos y ejecutamos tests en AuthApp CI.
> **Última actualización**: 2026-07-02

## Stack

- **Framework de tests**: JUnit 4 (ejecutado vía Maven Surefire).
- **Cobertura**: no configurada aún. A futuro se puede integrar JaCoCo (`jacoco-maven-plugin`) para medir cobertura y publicarla en SonarQube.
- **Tests de sistema/E2E**: no aplica. AuthApp es una demo trivial de autenticación en memoria, sin API HTTP, base de datos ni frontend; no hay flujos E2E que probar.

## Tipos de test

| Tipo      | Qué cubre                 | Carpeta                                  |
| --------- | ------------------------- | ---------------------------------------- |
| Unitarios | Funciones/clases aisladas | `authapp/src/test/java/com/equipo/auth/` |

Actualmente existen dos clases de test unitario: `AppTest` y `AuthServiceTest`.

## Reglas

- Todo cambio funcional se acompaña de tests.
- Estructura **Arrange-Act-Assert** (AAA): preparar, ejecutar, verificar.
- Un test verifica **una** cosa; nombres descriptivos del comportamiento esperado.
- Los tests deben ser deterministas (sin dependencia de red, reloj o orden).
- La CI (Jenkins) ejecuta `mvn clean test` en el stage **Build y Test** ante cada cambio; los tests deben pasar para continuar el pipeline.

## Ejemplos

```java
public class AuthServiceTest {
    @Test
    public void loginDevuelveTrueConCredencialesValidas() {
        // Arrange
        AuthService auth = new AuthService();
        // Act
        boolean resultado = auth.login("admin", "1234");
        // Assert
        assertTrue(resultado);
    }
}
```

## Comandos útiles

```bash
cd authapp && mvn clean test   # Ejecutar todos los tests
```

> No hay modo watch: Maven no lo trae por defecto. Tampoco hay comando de
> cobertura por ahora (ver nota sobre JaCoCo en la sección Stack).

## Referencias

- [Documentación de JUnit 4](https://junit.org/junit4/).
- [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/).
