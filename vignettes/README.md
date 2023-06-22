# gonzalezivan90.github.io

This is a public web page

# <a id="Model"></a>Model {#model}

We are now ready to build a distribution model. *Wallace v2.0* provides two algorithm options; Maxent and BIOCLIM. For this vignette, we'll use Maxent, a machine learning method that can fit a range of functions to patterns in the data, from simple (i.e., straight lines) to complex (i.e., curvy or with lines that can change direction; these can get jagged if complexity is not controlled). For more details on Maxent, please consult the <a href="https://biodiversityinformatics.amnh.org/open_source/maxent/" target="_blank">Maxent website</a> abnd guidance text.\
Maxent is available to run through `maxnet` package or through Java with the `maxent.jar` option.
In the interest of time and to avoid Java-related issues, let's choose the following modeling options:

-   Choose maxnet

-   Select L, LQ, and H feature classes. These are the shapes that can be fit to the data:

    -   L = Linear, e.g. temp + precip\
    -   Q = Quadratic, e.g. temp\^2 + precip\^2\
    -   H = Hinge, e.g. piecewise linear functions, like splines (think of a series of lines that are connected together)\

-   Select regularization multipliers between 0.5 and 4 with a step value of 0.5.

    -   Regularization is a penalty on model complexity.\
    -   Higher values = smoother, less complex models. Basically, all predictor variable coefficients are shrunk progressively until some reach 0, when they drop out of the model. Only those variables with the greatest predictive contribution remain in the model.\

-   Keep "NO" selected for categorical variables. This option is to indicate if any of your predictor variables are categorical, like soil or vegetation classes.

    -   Had you loaded categorical variables, you would check here and then indicate which of the rasters is categorical.

-   Set Clamping? to "TRUE". This will clamp the model predictions (i.e., keep the environmental values more extreme than those present in the background data to within the bounds of the background data).

-   If you set Parallel? to "TRUE", you can indicate the number of cores for parallel processing.

We will construct a model for *Bassaricyon neblina*, but note that the Batch feature can be checked to run these selections for all species you have uploaded.  
Make sure *Bassaricyon neblina* is selected in the species menu and Batch is unchecked before hitting **Run**.

The 3 feature class combinations (L, LQ, H) x 8 regularization multipliers (0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4) = 24 candidate models. The hinge feature class (H) will enable substantial complexity in the response, so it takes a bit longer to run than the simpler models.
