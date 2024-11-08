function enviarWhatsApp() {
    const copo = document.getElementById('copos').value;
    const marmita = document.getElementById('marmitas').value;
    const adicionais = [];
    const acompanhamentos = [];

    // Campos de Endereço
    const rua = document.getElementById('rua').value;
    const bairro = document.getElementById('bairro').value;
    const numero = document.getElementById('numero').value;
    const complemento = document.getElementById('complemento').value;
    const cidade = document.getElementById('cidade').value;

    // Preços dos itens
    const precoCopo = {
        "Copo 300ml": 10.00,
        "Copo 400ml": 12.00,
        "Copo 500ml": 15.00
    };
    const precoMarmita = {
        "Marmita 300ml": 12.00,
        "Marmita 400ml": 14.00,
        "Marmita 500ml": 22.00
    };
    const precoAdicional = {
        "Morango": 3.00,
        "Kiwi": 3.00,
        "Oreo": 3.00,
        "Creme de Avelã": 3.00
    };

    let total = 0;
    const tipoPedido = copo !== "" ? copo : marmita;
    total += precoCopo[copo] || precoMarmita[marmita];

    // Verifica os adicionais selecionados
    if (document.getElementById('morango').checked) adicionais.push("Morango");
    if (document.getElementById('kiwi').checked) adicionais.push("Kiwi");
    if (document.getElementById('oreo').checked) adicionais.push("Oreo");
    if (document.getElementById('cremeAvela').checked) adicionais.push("Creme de Avelã");

    // Soma os preços dos adicionais
    adicionais.forEach(adicional => {
        total += precoAdicional[adicional] || 0;
    });

    // Soma os acompanhamentos (sem valores)
    if (document.getElementById('granola').checked) acompanhamentos.push("Granola");
    if (document.getElementById('leiteCondensado').checked) acompanhamentos.push("Leite Condensado");
    if (document.getElementById('banana').checked) acompanhamentos.push("Banana");
    if (document.getElementById('mm').checked) acompanhamentos.push("M&M");
    if (document.getElementById('pacoca').checked) acompanhamentos.push("Paçoca");
    if (document.getElementById('farinhaAmendoim').checked) acompanhamentos.push("Farinha de Amendoim");
    if (document.getElementById('jujuba').checked) acompanhamentos.push("Jujuba");
    if (document.getElementById('gotasChocolate').checked) acompanhamentos.push("Gotas de Chocolate");

    // Adiciona a taxa de entrega
    const taxaEntrega = 3.00;
    total += taxaEntrega;

    // Formatação do texto para WhatsApp, com quebras de linha
    const textoPedido = `Pedido: ${tipoPedido}\nAdicionais: ${adicionais.length > 0 ? adicionais.join(", ") : 'Nenhum'}\nAcompanhamentos: ${acompanhamentos.length > 0 ? acompanhamentos.join(", ") : 'Nenhum'}\n\nEndereço de entrega:\nRua: ${rua}\nBairro: ${bairro}\nNúmero: ${numero}${complemento ? '\nComplemento: ' + complemento : ''}\nCidade: ${cidade}\nTaxa de entrega: R$3,00\n\nTotal: R$ ${total.toFixed(2)}`;

    const urlWhatsApp = `https://wa.me/55<81991702554>?text=${encodeURIComponent(textoPedido)}`;
    window.open(urlWhatsApp, '_blank');
}
