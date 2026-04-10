# home-dns-dhcp

flowchart TD

    %% Internet
    Internet((Internet)) -->|Fiber/Cable| Xfinity

    %% Gateway Layer
    subgraph Gateway_L3 [Gateway (L3)]
        Xfinity[Xfinity Gateway\n10.0.0.1\n(Router Mode)]
    end

    %% Core Services
    subgraph Core_L2L4 [Core Services (L2/L4)]
        MacMini[Mac Mini M1\n10.0.0.4]

        AdGuard[AdGuard Home\nDNS & AdBlock]
        Kea[ISC Kea DHCP\nDHCP Server]

        AdGuard --> MacMini
        Kea --> MacMini
    end

    %% Access Layer
    subgraph Access_L1L2 [Access Layer (L1/L2)]
        Deco[TP-Link Deco\n(AP Mode)]

        iPhone[iPhone]
        Tesla[Tesla]
        IoT[Smart Home Devices]
    end

    %% Connections
    Xfinity -->|NAT| MacMini
    MacMini -->|DNS: 10.0.0.4| Deco
    MacMini -->|DHCP: 10.0.0.4| Deco

    Deco --> iPhone
    Deco --> Tesla
    Deco --> IoT
