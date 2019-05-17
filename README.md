# AngularCommunication3

## Comunicación a través del servicio.
Finalmente, esta opción es útil y se debe utilizar cuando tenga un componente controlado o se pregunte su estado desde varias instancias.

![alt text](https://cdn-images-1.medium.com/max/800/1*c7F8p2e1Q2O8sIAEB9Pf5Q.png)

Ahora tenemos varios lugares en la aplicación que necesitarán acceder a nuestro componente de la barra lateral. A ver cómo lo hacemos.
Ahora crearemos side-bar.service.ts por lo que tendremos:
```
side-bar.service.ts
side-bar.component.ts
side-bar.component.html
```
Los servicios de la barra lateral tendrán un método de alternar y un evento de cambio para que cada componente que inyecte este servicio pueda recibir una notificación de que el panel se abrió o puede activarlo.
En este ejemplo, ni el componente de la barra lateral ni el componente de barra lateral tienen parámetros de entrada, ya que se comunican a través del servicio.
Ahora el código:

### app.component.html
```html
<app-side-bar-toggle></app-side-bar-toggle>
<app-side-bar></app-side-bar>
```
### side-bar-toggle.component.ts
```typescript
@Component({
  selector: 'app-side-bar-toggle',
  templateUrl: './side-bar-toggle.component.html',
  styleUrls: ['./side-bar-toggle.component.css']
})
export class SideBarToggleComponent {

  constructor(
    private sideBarService: SideBarService
  ) { }

  @HostListener('click')
  click() {
    this.sideBarService.toggle();
  }
}
```
### side-bar.component.ts
```typescript
@Component({
  selector: 'app-side-bar',
  templateUrl: './side-bar.component.html',
  styleUrls: ['./side-bar.component.css']
})
export class SideBarComponent {

  @HostBinding('class.is-open')
  isOpen = false;

  constructor(
    private sideBarService: SideBarService
  ) { }

  ngOnInit() {
    this.sideBarService.change.subscribe(isOpen => {
      this.isOpen = isOpen;
    });
  }
}
```
### side-bar.service.ts
```typescript
@Component({
  selector: 'app-side-bar',
  templateUrl: './side-bar.component.html',
  styleUrls: ['./side-bar.component.css']
})
export class SideBarComponent {

  @HostBinding('class.is-open')
  isOpen = false;

  constructor(
    private sideBarService: SideBarService
  ) { }

  ngOnInit() {
    this.sideBarService.change.subscribe(isOpen => {
      this.isOpen = isOpen;
    });
  }
}
```
Las importaciones se omiten en el código de TypeScript 

Este proyecto se generó con [Angular CLI] (https://github.com/angular/angular-cli) versión 1.3.0.

## Development server

Ejecute `ng serve` para un servidor dev. Vaya a `http://localhost:4200/`. La aplicación se volverá a cargar automáticamente si cambia alguno de los archivos de origen.

## Code scaffolding

Ejecute `ng generar componente nombre-componente` para generar un nuevo componente. También puede usar`ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Ejecuta `ng build` para construir el proyecto. Los artefactos de compilación se almacenarán en el directorio `dist /`. Use la bandera `-prod` para una compilación de producción.

## Running unit tests

Ejecute `ng test` para ejecutar las pruebas unitarias a través de [Karma] (https://karma-runner.github.io).

## Running end-to-end tests

Ejecute `ng e2e` para ejecutar las pruebas de extremo a extremo a través de [Protractor] (http://www.protractortest.org/).
Antes de ejecutar las pruebas, asegúrese de que está sirviendo la aplicación a través de `ng serve`.

## Further help

Para obtener más ayuda sobre Angular CLI, use `ng help` o visite el [Angular CLI README] (https://github.com/angular/angular-cli/blob/master/README.md).
