<img src="../decentralized virtual private network.png" alt="Arkham dVPN for DAWN" />

# Arkham dVPN

### A Decentralized, User-Owned VPN for the DAWN Black Box

-----

## About The Project

Arkham is a decentralized, user-owned VPN (dVPN) built exclusively for the DAWN Black Box ecosystem. It transforms the distributed network of Black Boxes into a powerful tool for digital sovereignty and privacy. By activating "The Veil," users can route their internet traffic through other peer nodes on the network, effectively cloaking their digital identity from ISPs, advertisers, and other centralized entities.

Drawing inspiration from cypherpunk ethos, Arkham uses strong, trustless cryptography to rewrite the rules of the internet in favor of the individual. Users can choose to be a **Seeker** (routing their traffic through the network for privacy) or a **Warden** (sharing their spare bandwidth as an exit node to strengthen the network).

Arkham isn't just a utility; it's a foundational layer for the user-owned internet DAWN envisions. It provides a direct, tangible benefit to every Black Box owner, making the entire network more resilient, private, and valuable with each new participant.

## Arkham & The DAWN Black Box

Arkham is designed to be a core service running inside every DAWN Black Box. By packaging the Go backend into a lightweight, self-contained Linux container, it can be deployed seamlessly to the Black Box hardware.

This project directly answers the call of the DAWN bounty by creating a functional, cypherpunk utility that leverages the distributed nature of the Black Box network. It turns a collection of individual Black Boxes into a powerful, cohesive, and privacy-preserving dVPN for the entire community, adding immense value to every device owner.

### Built With

<img src="../decentralized virtual private network tools.png" alt="Arkham Tools"/>

This project is a monorepo containing two main packages:

  * **Backend:**
      * [Go](https://go.dev/)
      * [go-libp2p](https://github.com/libp2p/go-libp2p) for peer-to-peer networking
      * [go-wireguard](https://git.zx2c4.com/wireguard-go/) for VPN tunneling logic
  * **Frontend:**
      * [Next.js](https://nextjs.org/)
      * [React](https://reactjs.org/) & [TypeScript](https://www.typescriptlang.org/)
      * [Tailwind CSS](https://tailwindcss.com/)
      * [shadcn/ui](https://ui.shadcn.com/) for UI components
      * [Vercel](https://vercel.com/) for deployment

-----

## Getting Started

To get a local copy up and running, follow these steps.

### Prerequisites

You must have the following tools installed on your system.

  * **Go** (version 1.21 or later)
  * **pnpm** (or npm/yarn)
    ```bash
    npm install -g pnpm
    ```
  * **WireGuard Tools**
      * On Arch Linux (like the development environment):
        ```bash
        sudo pacman -S wireguard-tools
        ```
      * On Debian/Ubuntu:
        ```bash
        sudo apt install wireguard-tools
        ```

### Running the Application Locally

The easiest way to run Arkham locally is with the `ArkhamCLI`. It provides an interactive menu to manage your nodes. You will need at least two nodes running to test the network: one Gateway and one Peer.

1.  **Build the CLI**
    First, compile the CLI into an executable.

    ```bash
    cd arkham-cli
    go build -o arkham
    ```
    This will create an `arkham` executable in the `arkham-cli` directory.

2.  **Start the Gateway Node (Terminal 1)**
    The Gateway Node runs the main P2P services and the API server for the web dashboard. It requires `sudo` to manage network interfaces.

    ```bash
    cd arkham-cli
    sudo ./arkham
    ```
    From the interactive menu, select **"Start Gateway Node"**.

3.  **Start a Peer Node (Terminal 2)**
    This node acts as a peer for the Gateway to connect to. Open a new terminal for this process.

    ```bash
    cd arkham-cli
    ./arkham
    ```
    From the interactive menu, select **"Start Peer-Only Node"**.

4.  **Start the Frontend (Terminal 3)**
    This will start the Next.js development server for the UI.

    ```bash
    cd arkham-vpn
    pnpm install
    pnpm dev
    ```

### Usage

1.  With all three processes running, open your web browser and navigate to **[http://localhost:3000](http://localhost:3000)**.
2.  Click through to the dashboard.
3.  The "ACTIVE NODES" card should show `1` or more as peers are discovered.
4.  Hover over the dots on the map to see peer details in a tooltip.
5.  Click the large **"Activate The Veil"** button.
6.  The UI will update to a "Secured" state, and the backend will create a `wg0` network interface on your machine, proving the VPN tunnel was successfully negotiated and configured. You can verify this by running `ip addr show wg0` in a new terminal.

-----

## Author

Skipp | [GitHub](https://github.com/DavidNzube101) | [X](https://x.com/davidnzubee)

-----


## License

Distributed under the MIT License. See `LICENSE` for more information.
