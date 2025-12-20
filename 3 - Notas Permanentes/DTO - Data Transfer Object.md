---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Definición

El objeto de transferencia de datos -DTO es un objeto cuyo único propósito es **mantener valores**.

No contiene **lógica de negocio**, solo atributos y, opcionalmente, getters/setters.

```java
public class PersonDto {
    private final String firstName;
    private final String lastName;
    private final int age;

    public PersonDto(String firstName, String lastName, int age) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
    }
    // métodos básicos como getters
}
```

---

# Flujo De Un DTO En la Arquitectura

## Creación

- El DTO nace en la frontera del sistema:
    - Desde la **Vista (UI)**: por ejemplo, un formulario que captura datos de un usuario.
    - Desde una **API externa**: al recibir una request en formato JSON/XML, se convierte a DTO.

## Recepción En la Facade / Controlador

- El DTO llega al **Facade** o al **Controlador** como un objeto de entrada.
- En esta capa no se trabaja con lógica de negocio, solo se recibe el mensaje.

## Transformación DTO → Dominio

- Un **Mapper** convierte el DTO en un **objeto de dominio** (clase con lógica).
- Ejemplo: `UsuarioDTO` se convierte en `Usuario`.

## Uso En El Caso De Uso

- El **Caso de Uso** trabaja con el objeto de dominio real.
- Aquí se aplican validaciones, reglas de negocio, cálculos y persistencia.

## Transformación De Vuelta Dominio → DTO

- El resultado se convierte nuevamente en DTO para devolverlo hacia la UI o la API externa.
- El DTO de salida es liviano y fácil de serializar.
    
---

# Ejemplo: Traducción De Un Artículo

![[DTO - Data Transfer Object-1759372365980.webp]]

```java title:"Objeto DTO"
public class ArticleDto {
	private final LocalDate date;
	private final String text;
	public ArticleDto( LocalDate date, String text)
	{
		this. date = date;
		this. text = text;
	}
// métodos básicos como getters
}
```

```java title:"Objeto del Dominio"
public class Article {
	private final Translator translator;
	private LocalDate date;
	private String text;
	
	public Article(Translator translator, LocalDate date, String text) {
		this.translator = translator;
		this.date = checkNotNull(date);
		this.text = nullToEmpty(text);
    }
    
	public void translate(Language language) {
		text = translator.translate(text, language);
    }
}

public class Translator {
	public String translate(String toTranslate, Language language) {
	// do translation
	return translated;
    }
}
```

``` java title:"El Caso de Uso"
public class TranslateArticleUseCase {

	private final ArticleMapper mapper;
	
	public TranslateArticleUseCase(ArticleMapper mapper) {
        this.mapper = mapper;
    }
    
    public ArticleDto translateArticleUseCase(ArticleDto articleDto,             Language language) {
        Article article = mapper.transform(articleDto);
        // Domain //
        article.translate(language);
        // End of Domain //
        ArticleDto resultDto = mapper.transform(article);
        return resultDto;
    }
}
```

---

# Ventajas Del Uso De DTOs

- Evitan exponer directamente las clases de dominio.
- Reducen acoplamiento entre capas.
- Son ligeros y fáciles de transportar (incluso entre procesos o servicios).
- Son fáciles de serializar (JSON, XML, etc).
- Permiten devolver solo la información necesaria, ocultando detalles internos.
