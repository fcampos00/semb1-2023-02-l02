# Atividades de Laboratório - Sistemas Embarcados I

# Felipe Andrade Campos - 11921ETE007

1. O programa disponibilizado na pasta **stm32f411-blackpill** pisca o LED conectado ao pino PC13 no kit STM32F411 Blackpill. Faça um *fork* deste repositório e altere o programa para que, ao se pressionar o botão conectado a PA0 o LED fique aceso e, ao soltar este botão, o LED se apague.

Segue o código em anexo:

int main(void)
{
    // Configurar o pino PA0 como entrada
    RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN; GPIOA->MODER &= ~GPIO_MODER_MODER0;

    // Configurar o pino PC13 como saída
    RCC->AHB1ENR |= RCC_AHB1ENR_GPIOCEN; GPIOC->MODER |= GPIO_MODER_MODER13_0;

    // Variável para controlar o estado do LED
    int ledLigado = 0;

    while (1)
    {
        // Ler o estado do botão (PA0)
        if (GPIOA->IDR & GPIO_IDR_IDR_0)
        {
            // Botão pressionado: alternar o estado do LED
            if (ledLigado)
            {
                GPIOC->BSRR = GPIO_BSRR_BR_13; // Apagar o LED
                ledLigado = 0;
            }
            else
            {
                GPIOC->BSRR = GPIO_BSRR_BS_13; // Acender o LED
                ledLigado = 1;
            }

            // Aguardar um breve intervalo para evitar leituras múltiplas
            for (volatile int i = 0; i < 100000; ++i)
            {
                // Espera
            }
        }
    }
}

3. Faça um novo *fork* deste repositório e altere o programa para que, ao se pressionar o botão conectado a PA0 o estado do LED seja trocado, ou seja, caso o LED esteja apagado ao se pressionar o LED uma vez o mesmo deve acender ao pressionar o botão o LED deverá apagar.

Segue o código em anexo:

  
  int main(void)
{
    // Configurar o pino PA0 como entrada
    RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN; GPIOA->MODER &= ~GPIO_MODER_MODER0;

    // Configurar o pino PC13 como saída
    RCC->AHB1ENR |= RCC_AHB1ENR_GPIOCEN; GPIOC->MODER |= GPIO_MODER_MODER13_0;

    // Variável para controlar o estado do LED
    int ledLigado = 0;

    while (1)
    {
        // Ler o estado do botão (PA0)
        if (GPIOA->IDR & GPIO_IDR_IDR_0)
        {
            // Botão pressionado: alternar o estado do LED
            if (ledLigado)
            {
                GPIOC->BSRR = GPIO_BSRR_BR_13; // Apagar o LED
                ledLigado = 0;
            }
            else
            {
                GPIOC->BSRR = GPIO_BSRR_BS_13; // Acender o LED
                ledLigado = 1;
            }

            // Aguardar um breve intervalo para evitar leituras múltiplas
            for (volatile int i = 0; i < 100000; ++i)
            {
                // Espera
            }
        }
    }
}
