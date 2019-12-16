<h1>Installing the API to a Local Machine</h1>
<ol>
    <li>
        <h3>Initial Installation</h3>
        <ul>
            <li>Ensure you are installing on a Kali Linux Machine.</li>
            <li>Download the zip file or clone directly to your preferred directory.</li>
            <li>Make sure there is internet connection on the Kali Machine at all times.</li>
            <li>After downloading, go to the downloaded directory (i.e., inside the new downloaded directory.</li>
            <li>Make sure you have <em>extensions.txt, fasttrack.txt, metasploit, pswds.lst, url.txt and user.txt</em>
                in the downloaded directory.</li>
                        <li>
                <strong>Nmap-Vulners Installation:</strong> 
                <ul>
                    <li>Go to this link: <a href="https://github.com/vulnersCom/nmap-vulners">Nmap-Vulners</a></li>
                    <li>Download the repository locally.</li>
                    <li>Follow the steps in the Installation section, it's simple and straightforward.</li>
                    <li>You will need to locate the hidden <em>.nmap</em> directory on the Kali machine. If you cannot find this directory then it is probably in <em>/usr/share/nmap/scripts</em> directory.</li>
                    <li>Copy the <em>nmap-vulners.nse</em> script here. </li>
                </ul>   
            </li>
            <li>
                <strong>Vulscan Installation</strong>
                <ul>
                    <li>Go to this link: <a href="https://github.com/scipag/vulscan">Vulscan</a></li>
                    <li>Follow the steps in the <em>Installation</em> section.</li>
                    <li>This should take place in the same nmap scripts directory as above in nmap-vulners.</li>
                </ul>
            </li>
        </ul>
    </li>
    <li>
        <h3>Pre-run Configurations</h3>
        <ul>
            <li>Inside the API directory, open a terminal and enter <strong><em>npm install</em></strong>. This will
                install all node dependencies required.</li>
            <li><strong>DO NOT MODIFY THE <em>.env</em> FILE </strong> with any of your own paths.</li>
            <li>Any of the <em>passwordlists and extension files</em> inside the API can be modified to reflect what you
                want. However it is <strong>recommended to not do so</strong>
                because they already contain good estimates of what is required.</li>
            <li>Finally, inside the API in a terminal, enter <strong>node pentestApi.js</strong> and hit enter.</li>
            <li>Make sure the console output says <em>Server has started</em>, this means that The API has now started,
                and is waiting for connections.</li>
            <li><strong>NOTE:</strong> The API runs on port 3005, and normally you shouldn't have anything running on
                this port. If you do get an error, make sure that
                there is no process running on port 3005 and kill such a process!</li>
        </ul>
    </li>
    <li>
        <h3>Sending Requests to the API</h3>
        <ol type="I">
            <li>
                <h4>HTTP Requests</h4>
                <ul>
                    <li>A request can be sent from anywhere in the form of an HTTP request, i.e., from inside code, from
                        a
                        platform or simply from a terminal in the form of
                        <strong>http://hostaddress:port/starttest/192.168.1/startIP/endIP/phases</strong>.</li>
                    <li>A sample request looks like the following - <br> <strong>curl
                            http://localhost:3005/starttest/192.168.1/212/212/ivd</strong> <br>
                        <ol>
                            <li>
                                In this example we used the curl command to send a request to a RESTful HTTP route. We
                                used
                                <em>localhost</em> because we sent the request from the
                                same machine, in other cases acquire the IP Address of the Kali Machine and send a
                                request to
                                that IP, followed by the port.
                            </li>
                            <li>
                                The route parameters include the <em>startest</em> keyword followed by the local subnet
                                which is
                                <em>192.168.1</em> in most cases.
                            </li>
                            <li>
                                This is followed by a start IP address, in this case start from 192.168.1.212. The next
                                parameter is the end IP Address. In this case its the same
                                device. This means it only pen-tests one device. <br>
                                The last parameter is to specify the phases of testing, which for now need to include
                                all 3
                                phases, <br>
                                i -> Information Gathering <br>
                                v -> Vulnerabililty Assessment <br>
                                d -> Dictionary Attacks
                            </li>
                        </ol>
                    </li>
                </ul>
            </li>
            <li>
                <h4>MQTT Requests</h4>
                <ul>
                    <li>A request can be sent from anywhere in the form of an MQTT request, i.e., from inside code, from a platform or from any MQTT client.</li>
                    <li>The requirements for the MQTT client are:-
                        <ol>
                            <li>It should connect to the online broker at <strong>broker.hivemq.com</strong> and if the client is a server then it would require the <em>TCP port 1883</em> otherwise if it's a Websocket like in Angular it would require <em>Websocket port 8000
                            </em>.</li>
                            <li>The client can be created using MQTT libraries on any platform whether it's Vanilla JS or Angular JS or Typescript.</li>
                            <li>An example of creating an MQTT client in Vanilla JS is shown in the <strong><em>portal.html</em></strong> file in this directory.</li>
                            <li>It connects to the broker, then subscribes to the required topics which are <strong>"pentest/updates"</strong> and <strong>"pentest/complete".</strong></li>
                            <li>Any other client should also subscribe to these topics to receive updates and notifications.</li>
                            <li>As shown in the <em>portal.html</em> file the <em>startPenTest()</em> starts the pen test by publishing on the <strong>"pentest/start"</strong> topic.</li>
                            <li>The API is listening on this topic, and after receiving a message on this topic, it begins the test.</li>
                            <li>The format of the start message is as shown in the portal file i.e., a <strong>comma seperated list of IPs without the beginning <em>192.168.1.</em></strong> </li>
                        </ol>
                    </li>
                    <li>Once the test is complete, you will get a directory with the device's results as is the case with HTTP requests on the same Kali Machine.</li>
                    <li>The <em>portal.html</em> file can be used as a live demo of the MQTT functionality, it also does not have to face any CORS issues.
                    </li>
                    <li>Next update: Report generation (Not yet added).</li>
                </ul>
            </li>
        </ol>
    </li>
</ol>