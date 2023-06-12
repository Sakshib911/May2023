# Data Packet Corruption Detection
* In a Wireless communciation device, multiple data packets are transferred over the air. 
* It is possible that data might get corrupted or lost before it reaches the destination.
* Create a method to identify if a data packet is corrupted
* Assume below format for the data packet

#include <stdio.h>
#include <stdint.h>
#include <stddef.h>

#define MAX_PACKET_DATA_LENGTH (50)

typedef struct data_packet_t {
    uint8_t id;
    uint8_t data_length;
    uint8_t data[MAX_PACKET_DATA_LENGTH];
    uint32_t crc;
} data_packet_t;

uint32_t calculate_crc32(const void* data, size_t length) {
    // CRC32 calculation algorithm
    // You can use a library or implement it manually
    return 0;
}

int is_packet_corrupted(const data_packet_t* packet) {
    uint32_t calculated_crc = calculate_crc32(packet, sizeof(data_packet_t) - sizeof(uint32_t));
    return (calculated_crc != packet->crc);
}

int main() {
    data_packet_t packet;
    packet.id = 1;
    packet.data_length = 10;
    for (int i = 0; i < packet.data_length; i++) {
        packet.data[i] = i;
    }
    packet.crc = calculate_crc32(&packet, sizeof(data_packet_t) - sizeof(uint32_t));

    if (is_packet_corrupted(&packet)) {
        printf("Packet is corrupted.\n");
    } else {
        printf("Packet is not corrupted.\n");
    }

    return 0;
}
