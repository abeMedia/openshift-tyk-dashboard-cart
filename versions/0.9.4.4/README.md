# Tyk Dashboard v0.7 (BETA)

Tyk Dashboard enables the management of the Tyk API Gateway server via an interface and processes analytics data for reporting.

## Installation and Setup

1. Unzip the tarball to a preferred directory (it is self contained, place anywhere on your server)
2. Edit the tyk_analytics.conf file
    - Set the `tyk_api_config` section to match your Tyk Instance settings, this can reference a load balanced downstream point or direct at one of your running instance
    - Set the MongoDB connection string to be the same as those used by your Tyk instance
    - Set the Redis details to be the same as those used by your Tyk gateway
    - Enable or disable `notify_on_change` - only useful if you have the hot-reload agent installed
    - ensure the License holder name is the same as that which you set your License up with
    - place your license file into the same directory as the conf file
3. Open a terminal and run: `./tyk-analytics --neworg --newuser`, this will create a base organisation and your first admin user, follow the instructions on screen. *NOTE*: The Organisation name should only be one word (bug).
4. Once complete, tyk should be running. We recommend killing th process now as you will want to start Tyk with a license, so press Ctrl-C to kill the process

**To start the tyk dashboard run:** `./tyk-analytics --license=license.dat`

This assumes you have a license, if you don't then omit the `license` flag, tyk should start up and you should not be able to access the server at `http://localhost:3000/` and access it with the user and password
you created in step 3.

## The Host Manager

If you want to be able to dynamically load your API configurations from the dashboard (and not call the `/reload` endpoint manually for each tyk instance)
It is recommneded to run the Tyk Host Manager, which automates this task for you. This is a licensed feature, it is quick to set up, and full
instructions can be found in the `TYK_HOST_MANAGER_README.md` file.

## Notes:

- Tyk Dashboard requires your Tyk instances to be configured to use database-backed API Definitions, if you are using a file-based setup the API management functionality will not work
- Hot reloads only work if `notify_on_change` and a hot-reload agent is installed on the same host as the tyk gateway processes, if you do not use the hot reload agent then you will need to call the `/reload` endpoint on the tyk instances manually

## Issue Reporting

We've set up a mailing list / google group for the Beta Users of Tyk Dashboard - if you would like to post bugs, feature requests, thoughts or ideas, please do so here:

[https://groups.google.com/forum/#!forum/tyk-dashboard-beta-community](https://groups.google.com/forum/#!forum/tyk-dashboard-beta-community)

The group is invite only, if you could lket us know in the joining notes which beta user you are (company, name or email will do), we'll confirm your access.

To get your license key, please email us at info@jive.ly with the subject line: `TYK BETA LICENSE REQUEST` with your name and company as the body of the message, the
key is only valid for the named user, so please check for typos :-)

## License and Copyright

Tyk Dashboard is copyright Martin Buhr and Jively Ltd. It is proprietary software and should not be distributed or copied.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, 
BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT 
SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL 
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS 
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE 
OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.