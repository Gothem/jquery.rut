## jQuery.rut

Plugin de jQuery para formateo y validación de RUTs. Este plugin funciona sobre un input de tipo texto.

### Licencia

1. Este plugin y todo el código contenido en este repositorio está regido por la licencia MIT 

2. Este plugin también está a la venta bajo otras licencias. Para consultas, póngase en contacto con @pablomarambio en Twitter.

### Requisitos y limitaciones

- Para usar el plugin, inclúyelo en una página que cuente con jQuery 1.4+
- Por ahora, el plugin sólo funciona con un único input. Para cargar múltiples input se debe invocar el plugin `.rut()` por cada uno de ellos.
- Sólo funciona con inputs de tipo texto

### Uso

**Ejemplos.** Para probar la funcionalidad, descarga `jquery.rut.js` y `demo.html` en una misma carpeta y abre `demo.html`en un browser.

**General.** Para activar la funcionalidad, basta invocar el método `.rut()` en objeto jQuery

```javascript
// asumiendo que la página cuenta con un input[type='text'] con 
// id "rut", la siguiente línea activa el plugin en dicho input.
$("input#rut").rut();
```

**Formateo y validación.** Por omisión, el plugin formatea cuando se gatilla el evento 'blur' del input, esto es, cuando pierde foco. Para formatear o validar en otro evento, el plugin debe invocarse con un valor distinto de `'blur'` para las opciones `'formatOn'` y `'validateOn'`:

```javascript
// formateará el RUT cada vez que se escriba en el campo y
// validará cuando el texto haya cambiado
$("input#rut").rut({
	formatOn: 'keyup',
	validateOn: 'change' // si no se quiere validar, pasar null
});
```

**Eventos.** Cuando el plugin valida el RUT, gatilla uno de dos eventos: `rutValido` y `rutInvalido`. La página puede responder a estos eventos de la manera que encuentre apropiada. Por ejemplo,

```javascript
// muestra un mensaje de error cuando el rut es inválido
$("input#rut").rut().on('rutInvalido', function(e) {
	alert("El rut " + $(this).val() + " es inválido");
});
```

```javascript
// muestra un mensaje de alerta con el rut y el dígito 
// verificador cuando el RUT es válido
$("input#rut").rut().on('rutValido', function(e, rut, dv) {
	alert("El rut " + rut + "-" + dv + " es correcto");
});
```

Notar que cuando el rut es válido, la función recibe dos argumentos adicionales, el RUT y el dígito verificador. En este caso, el RUT no vendrá formateado.
