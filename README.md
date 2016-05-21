# nuclide-remote
The Nuclide-remote Docker container enables remote editing with Nuclide. This Dockerfile and corresponding docker image uses Watchman 4.5, Nuclide 0.138, and Node 6.2.

Further documentation about Nuclide can be found at:
http://nuclide.io/docs/remote/

### Connectivity

Communication between Nuclide and Nuclide-remote uses 2 ports:
- ssh/2222: needed to start nuclide remote inside Docker container
- 9090: the Nuclide communication channel

### Example

Setup access to a project at `/src` on a remote host on with etc host entry `nuclide`.
Ssh will be run over port `2222` and `9090` will be used by Nuclide for communication.

On the remote host start this Docker container. Prebuilt image `robzhu/nuclide-remote` available on Docker-Hub:

    sudo docker run -d -p 9090:9090 -p 2222:22 -v ~/src:/src robzhu/nuclide-remote

On the local machine start Nuclide, select *Packages/Connect..* and enter the connection information:

- Username: `root`
- Server: `nuclide`
- Initial Directory: `/src`
- Password: `nuclide`
- SSH Port: `2222`
- Remote Server Command: `nuclide-start-server -p 9090`

After pressing ok the remote directory will show up in navigator and will be ready for editing.
