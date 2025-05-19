# Expondo Aplicação Backend na Azure VM

Para acessar uma aplicação rodando na sua máquina virtual Azure pela internet, é necessário liberar a porta no firewall da Azure e garantir que sua aplicação esteja escutando no IP e porta corretos.

---

## ✅ Passo a Passo

### 1. Libere a Porta no Grupo de Segurança de Rede (NSG)

1. Acesse o [Portal Azure](https://portal.azure.com).
2. Vá até sua **Máquina Virtual > Rede > Grupo de segurança de rede**.
3. Em "Regras de segurança de entrada", clique em **Adicionar**.
4. Configure a regra:
   - **Origem**: Qualquer
   - **Porta de origem**: *
   - **Destino**: Qualquer
   - **Porta de destino**: `3000` (ou a porta da sua aplicação)
   - **Protocolo**: TCP
   - **Ação**: Permitir
   - **Prioridade**: 900
   - **Nome**: `permitir-app-backend`

---

### 2. Configure sua aplicação para escutar no IP público

Certifique-se de que sua aplicação backend (ex: Express, Fastify, etc) está escutando na porta correta e no IP `0.0.0.0`.

#### Exemplo com Node.js / Express:

```js
app.listen(3000, '0.0.0.0', () => {
  console.log('Servidor rodando em http://0.0.0.0:3000');
});
```
