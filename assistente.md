{
    "Comment": "Assistente de Delivery para AWS Step Functions",
    "StartAt": "ObterRequisitosDoPedido",
    "States": {
        "ObterRequisitosDoPedido": {
            "Type": "Pass",
            "Result": {
                "prompt": "Olá! Sou seu assistente de delivery. Para ajudar na sua refeição, preciso de alguns detalhes. Qual o tipo de refeição que você gostaria de fazer? (exemplo: jantar, almoço, encontro, lanche, etc.)"
            },
            "Next": "EscolherCategoriaDeComida"
        },
        "EscolherCategoriaDeComida": {
            "Type": "Pass",
            "Result": {
                "prompt": "Ótimo! Qual tipo de comida você prefere? Pode ser algo específico como italiano, japonês, mexicano, ou até mesmo um tipo de prato específico, como pizza, sushi ou tacos."
            },
            "Next": "EscolherBebida"
        },
        "EscolherBebida": {
            "Type": "Pass",
            "Result": {
                "prompt": "Para complementar a refeição, gostaria de uma sugestão de bebida? Temos desde opções de sucos, refrigerantes, até vinhos e drinks, dependendo do tipo de ocasião."
            },
            "Next": "ConfirmarPedido"
        },
        "ConfirmarPedido": {
            "Type": "Choice",
            "Choices": [
                {
                    "Variable": "$.confirmar",
                    "BooleanEquals": true,
                    "Next": "ProcessarPedido"
                },
                {
                    "Variable": "$.confirmar",
                    "BooleanEquals": false,
                    "Next": "ObterRequisitosDoPedido"
                }
            ],
            "Default": "Finalizar"
        },
        "ProcessarPedido": {
            "Type": "Pass",
            "Result": {
                "prompt": "Seu pedido foi confirmado e está sendo processado. Estamos preparando tudo conforme as suas preferências!"
            },
            "Next": "Finalizar"
        },
        "Finalizar": {
            "Type": "Succeed"
        }
    }
}
