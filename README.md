# Devops Challenge

# Assignment 1

Troubleshooting

The interface that integrates our system with that of our SMS Gateway partner started
to produce some weird intermittent errors recently.
Here is how the process works:
1) Periodically, we run a program called generate_data, which generates a number of files that
are stored in /opt/sms/AU/mo

2) Also periodically, we run a program called process_data that processes these files and inte-
grates them into our system.

3) When we run process_data, the correct/expected output should be:
1. All files processed, or
2. Processing skipped

4) When an error occurs, the output is:

1. ERROR: Failed processing files.

To trigger the issue you can run the following from the command line:
generate_data && process_data
Running this a few times in a row should definitely trigger the mentioned error.
Can you:
1) Explain what causes the intermittent error?
2) Fix the intermittent error?
3) Explain the steps you took troubleshooting this intermittent error?
