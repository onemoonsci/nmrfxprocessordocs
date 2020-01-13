### active

Get or set the active chart. By default, the currently active chart is the last created or last one
that the mouse was clicked in.  When getting the active chart the command will return a name.
When setting the active chart the argument can be a name of a chart, in which case it is specified as a string (i.e. in quotes),
or it can be a number, in which case it is an index into the number of charts in the current stage (counting from 0).

By default, and somewhat confusingly, the name of a chart is actually a string representation of an index of the total number of charts created.
So the first chart ever created is named "1", the second "2", etc.



Examples:

       aChart = nw.active()
       nw.active('4')  # Set the active chart to be the one named '4'
                       # (the fourth chart ever created in this session)
       nw.active(3)    # Set the active chart to be the one with index
                       # (counting from 0) 3, within this stage.

One could loop over all the charts in a stage with something like:

    for iChart in range(nw.nCharts()):
        nw.active(iChart)
        nw.config(lvl=0.5)



### axlim

Set plot limit for a specified axis

Examples:

       nw.axlim('x',6.0,9.0)


### center

Centers chart on a specified position.  If no arguments are given the position is that of the crosshairs.
 
Examples:

    nw.center()             # center on crosshair position
    nw.center(8.55)         # center on an x value of 8.55
    nw.center(8.55,174)     # center on an x value of 8.55 and y value of 174.0
    nw.center(x=8.60)       # center on an x value of 8.60
    nw.center(x=8.60,y=175) # center on an x value of 8.60 and y value of 175.0

### colors

Currently applies to pseudo 2D datasets (an array of 1D datasets).  Allows user to specify a color used for specified rows.

Examples:

        nw.colors([3,4],'blue')   Set rows 3 and 4 (starting at 0) to be colored blue

### config

Configure parameters of active chart.  With no arguments returns a dictionary of parameters currently set on chart.

Examples:
    
     nw.config()
        neg: true, negWidth: 0.5, lvl: 1.8488425889503632, clm: 1.2, pos: true, posColor: #000000FF, negColor: #FF0000FF, posWidth: 0.5, nlvls: 20}

     nw.config(lvl=2.0)

### datasets

Get or set the list of datasets in the active chart.  A given chart can have multiple datasets so the datasets are set and returned as python lists.

Examples:

    datasets = nw.datasets()

    nw.datasets(['hnco.nv'])

### draw

Redraw active chart

Examples:

    nw.draw()

### drawAll

Redraw all charts in active stage

Examples:

    nw.drawAll()



### expand

Expand chart to region in crosshairs

Examples:

    nw.expand()

### full

Show full spectrum in chart.  A dimension name can be specified so the full range is only done for that dimension.

Examples:

    nw.full()

    nw.full('y')


### geometry

Return or set the geometry (x, y, width, height) for the active stage.

Examples:

    geom = nw.geometry()

    nw.geometry(x=500,y=600, width = 400, height=500)

    nw.geometry(x=300,y=400)
   

### getCursor

Return the cursor used in the active chart (CROSSHAIR or MOVE)

Examples:

    nw.getCursor()

### getDAttrs

Gets a list of the DatasetAttributes in the active chart.  This is a low-level, command for advanced use.


### getDims

Get list of dataset dimensions (indices starting at 0) that are currently displayed on chart

Examples:

        dims = nw.getDims('hnco.nv')

### getGrid()

Get the current grid in the active stage
   
Examples:

      grid = nw.getGrid()

### grid

Create a grid of charts in current stage.  With no arguments resets the grid to a single chart.

Examples:

    nw.grid(rows=3,columns=2)

### lim
    Get or set the plot limits of current chart.

Examples:

       nw.lim()
           {x: [6.441539693970839, 9.495060306029162], y: [167.06294474318503, 182.93926565771682], z: [64.0, 64.0]}

       nw.lim(x=[4.0,7.0])

### nCharts

Return the number of charts in current stage.

Examples:

      n = nw.nCharts()


### new

Create new stage (toplevel window)

Examples:

    nw.new()

### offsets

Currently applies to pseudo 2D datasets (an array of 1D datasets).  Allows user to specify a vertical offset used for specified rows.

Examples:

        nw.offset([3,4],0.2)   Set rows 3 and 4 (starting at 0) to have an offset of 0.2 (as a fraction from 0 to 1.0)

### pconfig

Configure peak parameters of active chart.  With no arguments returns a dictionary of parameters currently set on chart.

Examples:

        nw.pconfig()
             simPeaks: false, displayType: Peak, offColor: 0xff0000ff, drawPeaks: true, labelType: Number, onColor: 0x000000ff}

        nw.pconfig(onColor='0xff0000')

### peakLists

Get or set the list of peaklists in the active chart.  A given chart can have multiple peaklists so the peaklists are set and returned as python lists.

Examples:

    peakLists = nw.peakLists()

    nw.peakLists(['hnco'])


### rows

Currently applies to pseudo 2D datasets (an array of 1D datasets).  Allows user to specify .which rows are displayed
   
        nw.rows([3,4])   Display rows 3 and 4.  All other rows are invisible.

### setDims

Set dataset dimensions (indices starting at 0) that should be displayed on chart)

Examples:

        nw.setDims('hnco.nv',[0,2,1])

### showPeak
    Jump chart display region to center on specified peak

Examples:

        nw.showPeak('hnco.32')
### stages

Should return a list of activew stages, but currently broken

### useActive

Set the active controller for the scripting commands to that of the active chart.  Advanced useage.

### zoom

Zoom in window according to specified factor

Examples:

       nw.zoom(1.1)
       nw.zoom(factor= 0.9)


