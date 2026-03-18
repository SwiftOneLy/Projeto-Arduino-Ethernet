<h1>1. Conectar o hardware</h1>
 <ul>
  <li>Conecte o Arduino ao módulo Ethernet.</li>
  <li>Utilize um cabo de rede (RJ45) para conectar o Arduino Ethernet ao roteador.</li>
  <li>Certifique-se de que todos os dispositivos estão ligados e funcionando corretamente.</li>
 </ul>

<h1>2. Reservar um endereço IP no roteador</h1>
 <ul>
  <li>Acesse o painel de administração do roteador (geralmente via navegador, por exemplo: 192.168.0.1 ou 192.168.1.1).</li>
  <li>Localize a seção de DHCP ou Reserva de IP.</li>
  <li>Identifique o Arduino pelo endereço MAC do módulo Ethernet.</li>
  <li>Configure uma reserva de IP (DHCP estático) para o Arduino, garantindo que ele sempre receba o mesmo IP na rede.</li>
  <li>Salve as configurações e, se necessário, reinicie o roteador.</li>
</ul>

<h1>3. Conectar o celular à rede</h1>
<ul>
<li>Conecte o celular à rede Wi-Fi do mesmo roteador.</li>
<li>Verifique se o celular recebeu um IP válido nas configurações de rede Wi-Fi.</li>
</ul>

<h1>4. Testar a comunicação</h1>
<ul>
<li>Utilize um aplicativo de terminal ou rede no celular (como PingTools, Termux, etc.).</li>
<li>Execute um comando de ping para o IP reservado do Arduino:</li>
<li>ping 192.168.X.X</li>
<li>(Substitua pelo IP configurado no roteador)</li>
<li>Se houver resposta, a comunicação entre o celular e o Arduino está funcionando corretamente.</li>
</ul>
<h4>Observação: nem todos os módulos Arduino respondem a ping. Caso não haja resposta, recomenda-se testar acessando via navegador (HTTP), se houver um servidor configurado no Arduino.</h4>

<h1>5. Validação e troubleshooting</h1>
<h3>Se a comunicação não funcionar, verifique:</h3>
<ul>
<li>Cabos e conexões físicas</li>
<li>Se o IP reservado está correto</li>
<li>Se o Arduino está programado corretamente com rede ativa</li>
<li>Reinicie o Arduino e o roteador</li>
<li>Verifique possíveis bloqueios de firewall na rede</li>
<li>Confirme se o celular e o Arduino estão na mesma faixa de IP (ex: 192.168.0.X)</li>
</ul>
