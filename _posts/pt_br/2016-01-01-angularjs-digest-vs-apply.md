---
layout: post

title: AngularJs - `$digest` vs `$apply`
tip-number: 01
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript modules e build steps estão ficando numerosos e complicados, mas e boilerplate e novos frameworks?

categories:
    - pt_br
---

Uma das características mais apreciadas do AngularJs é o two-way data binding. Para fazer este trabalho o AngularJs avalia as mudanças entre o model e a view através de ciclos ( $digest ). Você precisa entender esse conceito para entender como o framework funciona debaixo do capô.

Angular avalia cada observador quando um evento é disparado. Esse é o ciclo conhecido como `$digest`. Algumas vezes você precisa forçar a execução de um novo ciclo manualmente e deve escolher a opção correta pois esta fase é uma das que mais influencia em termos de performance.

### `$apply`
Este método do core permite você iniciar o ciclo digestion explicitamente. Isso significa que todos os observadores são verificados; toda a aplicação inicia o `$digest loop`. Internamente, depois de executar um parâmetro de função opcional, ele chama `$rootScope.$digest();`.

### `$digest`
Nesse caso o  método `$digest` inicia o ciclo `$digest` para o escopo atual e seu filhos. Você deve notar que os escopos pais não serão verificados e afetados.

### Recomendações
- Use `$apply` ou `$digest` somente quando os eventos DOM do navegador forem provocados fora do AngularJs.
- Passe uma expressão de função para `$apply`, ele tem um mecanismo de tratamento de erros e permite integrar as mudanças no ciclo digest.

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- Se você só precisa atualizar o escopo atual ou seus filhos, use `$digest`, previnindo um novo ciclo digest para toda a aplicação. O benefício em performance é evidente.
- `$apply()` é um processo difícil para a máquina e pode causar problemas de performance quando se tem muito binding.
- Se você está usando >AngularJS 1.2.X, use `$evalAsync`, um método do core que irá avaliar a expressão durante o ciclo atual ou o próximo. Isto pode melhorar a performance da aplicação.