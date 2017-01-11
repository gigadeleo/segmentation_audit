# segmentation_audit

When properly implemented, network segmentation is a method that can help reduce the number of system components in scope for PCI DSS.  segmentation_audit is a tool that identifies the level of access between out-of-scope networks and the audited PCI DSS in-scope environment by initially attempting to ping the destination environment, and then attempt to find out any open ports.

Follow [@gigadeleo](https://twitter.com/gigadeleo) on Twitter.

Installation Notes:
----------------------------------------------

segmentation_audit was designed to run with minimum system requirements. 
To run this tool you need to do the following:

  1. Copy 'segmentation_audit.sh' to a Linux directory of your choice.
  2. Give 'segmentation_audit.sh' execute rights.
  3. Copy 'ip-list' to the same directory; 'ip-list' is a list of in-scope IP addresses.
  4. Copy 'ports' to the same directory; 'ports' is a list of ports to scan in order to determine whether access between the host and the probed IP is open or not.

The script expects three (3) arguments:

  1. [FILE] Name of the ip-list file 
  2. [FILE] Name of the ports file
  3. [FLAG] Timeout Flag (0 - to use 'timeout' coreutils built-in shell function (timeout required); 1 - to use Perl Function (Perl required).
  
  Note: To know if your Linux host has timeout or perl install run:
  ```
  command -v timeout && echo "Available" || echo "Not Available"
  command -v perl && echo "Available" || echo "Not Available"
  ```
Usage Example:
  ```sh
  ./segmentation_audit.sh ip-list ports 0
  ```

Script in Detail:
----------------------------------------------
Copy the script to an 'out-of-scope' environment of your choice and run against IPs in the in-scope environment.
This will help you build a mesh / matrix of all access between the in-scope and out-of-scope environment.
This script is designed to run with minimum requirements and only uses bash, some basic built-in utilities (or Perl).

  1. Check whether all necessary files are available.
  2. Attempt to ping all of the in-scope IP Addresses.
  3. Attempt to run a simple port-scan on all hosts that return a ping response.
  4. Log all results in the log subdirectory.
  
----------------------------------------------
