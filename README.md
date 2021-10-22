# Projeto Loja Jordan

![Projeto loja Jordan](https://github.com/CarlosBaiao/storeJordan/blob/master/src/assets/imagesProject/project1.png?raw=true)


Este projeto foi desenvolvido com Vue.js, uma loja com alguns produtos que está sendo utilizado por meio de requisições, logo após tem a parte do carrinho com valor total e quantidade de produtos e por fim um formulário simulando uma compra.

### Aprendizados 
- Utilizar o Vue.Js
- Componentizaçao com Vue.js
- Utilizar rotas ( Vue router )
- Gerenciador de estado ( Vuex )
- Requisições ( Axios )
- Pré-processador css (Less)
- Responsividade 
- Manipular e tratar formulário 

## Sobre o projeto


![Carrinho vazio](https://github.com/CarlosBaiao/storeJordan/blob/master/src/assets/imagesProject/project2.png?raw=true)

Nessa parte do projeto é quando o carrinho é acessado ainda vazio, assim o valor total é ocultado e o botão de prosseguir é desabilitado.

![Carrinho com itens](https://github.com/CarlosBaiao/storeJordan/blob/master/src/assets/imagesProject/project3.png?raw=true)

Aqui o carrinho com produtos, assim o total aparece e o botão esta ativado, e os produtos são todos usados através de requisições com o Axios e quando um produto entra no carrinho ou é deletado, essa mudança ocorre pelo gerenciador de estado.


![Formulário de pagamento](https://github.com/CarlosBaiao/storeJordan/blob/master/src/assets/imagesProject/project4.png?raw=true)

Na parte de pagamento ocorre as validações, como nome e telefone e também o endereço precisa estar preenchido corretamente para finalizar a compra.

![Compra efetuada com sucesso](https://github.com/CarlosBaiao/storeJordan/blob/master/src/assets/imagesProject/project6.png?raw=true)

E se todos os dados estiverem de acordo, o usuário é redirecionado para a pagina de compra realizada, foi usado o vue router para fazer toda mudança de rotas e navegação pela pagina.
