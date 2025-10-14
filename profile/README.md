<img src="decentralized-virtual-private-network.png" alt="Arkham dVPN for DAWN" />

# Arkham dVPN

### A Decentralized, User-Owned VPN for the DAWN Black Box

-----

## About The Project

Arkham is a decentralized, user-owned VPN (dVPN) built exclusively for the DAWN Black Box ecosystem. It transforms the distributed network of Black Boxes into a powerful tool for digital sovereignty and privacy. By activating "The Veil," users can route their internet traffic through other peer nodes on the network, effectively cloaking their digital identity from ISPs, advertisers, and other centralized entities.

Drawing inspiration from cypherpunk ethos, Arkham uses strong, trustless cryptography to rewrite the rules of the internet in favor of the individual. Users can choose to be a **Seeker** (routing their traffic through the network for privacy) or a **Warden** (sharing their spare bandwidth as an exit node to strengthen the network).

Arkham isn't just a utility; it's a foundational layer for the user-owned internet DAWN envisions. It provides a direct, tangible benefit to every Black Box owner, making the entire network more resilient, private, and valuable with each new participant.

### Built With

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

To see the full end-to-end application in action, you need to run three processes in separate terminals: two backend nodes and the frontend web server.

1.  **Start the Main Backend Node (Terminal 1)**
    This node will run the P2P services and the API server on port `8080`. It requires `sudo` to create the WireGuard network interface.

    ```bash
    cd arkham-backend
    sudo go run .
    ```

2.  **Start the Peer-Only Backend Node (Terminal 2)**
    This node acts as a peer for the main node to connect to. The `-peer-only` flag prevents it from trying to start a conflicting API server.

    ```bash
    cd arkham-backend
    go run . -peer-only
    ```

3.  **Start the Frontend (Terminal 3)**
    This will start the Next.js development server for the UI on port `3000`.

    ```bash
    cd arkham-vpn
    pnpm install
    pnpm dev
    ```

### Usage

1.  With all three processes running, open your web browser and navigate to **[http://localhost:3000](https://www.google.com/search?q=http://localhost:3000)**.
2.  Click through to the dashboard.
3.  The "ACTIVE NODES" card should show `1` or more as peers are discovered.
4.  Hover over the dots on the map to see peer details in a tooltip.
5.  Click the large **"Activate The Veil"** button.
6.  The UI will update to a "Secured" state, and the backend will create a `wg0` network interface on your machine, proving the VPN tunnel was successfully negotiated and configured. You can verify this by running `ip addr show wg0` in a new terminal.

-----

## Deployment

  * **Frontend:** The `arkham-vpn` directory is a standard Next.js application ready for deployment on **Vercel**. When importing the project to Vercel, ensure you set the **Root Directory** to `arkham-vpn`.
  * **Backend:** The `arkham-backend` is a self-contained Go application. It can be built into a static binary (`go build`) and deployed in a **Linux container** or on any **VPS**. It must be run with `sudo` or as a user with `CAP_NET_ADMIN` capabilities to manage network interfaces.

> **Note:** For a real deployment, the `fetch` URL in the frontend code must be updated to point to the public IP of the deployed backend server, and the backend's CORS policy should be updated to allow requests only from the frontend's domain.

-----

## License

Distributed under the MIT License. See `LICENSE` for more information.
