# Wireshark

## Filtering Operators

Wireshark's filter syntax can be simple to understand making it easy to get a hold of quickly. To get the most out of these filters you need to have a basic understanding of boolean and logic operators.

Wireshark only has a few that you will need to be familiar with:

    and - operator: and / &&
    or - operator: or / ||
    equals - operator: eq / ==
    not equal - operator: ne / !=
    greater than - operator: gt /  >
    less than - operator: lt / <

## Basic Filtering

Filtering by IP: The first filter we will look at is ip.addr, this filter will allow you to comb through the traffic and only see packets with a specific IP address contained in those packets, whether it be from the source or destination.

`Syntax: ip.addr == <IP Address>`

Filtering by SRC and DST: The second filter will look at is two in one as well as a filter operator: ip.src and ip.dst. These filters allow us to filter the traffic by the source and destination from which the traffic is coming from.
``
``Syntax: `ip.src == <SRC IP Address> and ip.dst == <DST IP Address>`

