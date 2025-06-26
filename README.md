#include <avr/io.h>
#include <util/delay.h>

void setup() {
    // Set PB0, PB1, PB2 as output (Red, Yellow, Green LEDs)
    DDRB |= (1 << PB0) | (1 << PB1) | (1 << PB2);
}

void turn_off_all() {
    PORTB &= ~((1 << PB0) | (1 << PB1) | (1 << PB2));
}

void turn_on(uint8_t pin) {
    turn_off_all();
    PORTB |= (1 << pin);
}

int main(void) {
    setup();

    while (1) {
        turn_on(PB0);           // RED
        _delay_ms(5000);

        turn_on(PB1);           // YELLOW
        _delay_ms(2000);

        turn_on(PB2);           // GREEN
        _delay_ms(5000);

        turn_on(PB1);           // YELLOW before returning to RED
        _delay_ms(2000);
    }
}

