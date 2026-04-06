
### 1. Componentes: O Coração da Aplicação

Todo aplicativo Angular possui pelo menos um componente (o _root component_). Um componente controla uma "view" (uma parte da tela) e é composto por:

- **Uma Classe TypeScript:** Onde fica a lógica e os dados.
    
- **Um Decorator (`@Component`):** Metadata que diz ao Angular onde encontrar o HTML e o CSS desse componente.
    
- **Um Template HTML:** Que define como a interface será renderizada.

```Java
@Component({  
    selector: 'app-pagina',  
    standalone: true,  
    templateUrl: './pagina-componente.html',  
    styleUrls: ['./pagina-componente.scss'],  
    imports: [  
        CommonModule,  
        FormsModule,  
        ReactiveFormsModule,  
        FontAwesomeModule  
    ]  
})
``` 

### 2. Templates e Data Binding

O template é o HTML que o Angular usa para renderizar o componente. O diferencial é o **Data Binding**, que conecta seus dados à interface de forma automática:

- **Property Binding:** Envia valores do seu código para o HTML (ex: preencher um campo de texto).
    
- **Event Binding:** Responde a interações do usuário (ex: clicar em um botão) e executa uma função no código.
    
- **Two-way Binding:** Sincroniza os dois lados em tempo real (muito usado em formulários).
    
- **Diretivas:** Instruções no HTML que alteram a estrutura ou o estilo da página (como o `*ngIf` para mostrar algo condicionalmente ou `*ngFor` para listas).
    
- **Pipes:** Transformam dados antes de exibi-los (ex: formatar uma data ou moeda).