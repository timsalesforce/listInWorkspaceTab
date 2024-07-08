# Opening a list view in a workspace tab, and then using a VF page list button will not return correctly
# The retURL is not properly set.

This is an edge-case, but it can happen as demonstrated here.  It requires a custom VF button on the list view, and the VF page immediately returns to the previous page by calling StandarController.cancel().

## Repro

1. Clone this repository
2. Deploy to a scratch org (might need --force-overwrite)
3. Open the Account OH (list view)
4. Command click the list view (this should open the list view in a workspace tab)
5. Click on the "Account Quick List" button
6. Observe the VF page might blink but then immediately return to the list view

Also observe that when the cancel() action is processed, the retURL is to the VF page, and not the listview.  This causes the page to run again before it redirects back to the listview.  Luckily, on the second cancel() operation it makes it back to the listview.

The complaint by the customer is that the VF page runs twice and that messes with their logic.

If the retURL was set initially in objectHomeDesktop.cmp, then this problem is avoided.

