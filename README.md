StepView    [![](https://jitpack.io/v/siloamhospitals/StepView.svg)](https://jitpack.io/#siloamhospitals/StepView)
======================

A simple animated step view for Android. It displays the name of the step and an icon as index of the step with the state of the step (completed or not completed).

Usage
-----

1. Add jcenter() to repositories block in your gradle file.
2. Add `implementation 'com.github.siloamhospitals:StepView:1.5.4'` to your dependencies.
3. Add `StepView` into your layouts or view hierarchy.

Supported animations:

Name| Preview
-------- | ---
`ANIMATION_ALL`| ![animation_all](/images/ANIMATION_ALL.gif)
`ANIMATION_ALL and all next circles enabled`| ![animation_circles](/images/ANIMATION_CIRCLES.gif)

Usage:

Specify steps and number of steps so circles with step number and step name are shown with xml attribute:
```xml
	app:steps="@array/steps"
```
```java
	private List<Step> steps = new ArrayList<>();
        private List<String> listStepTitle = new ArrayList<>();
        
        listStepTitle = Arrays.asList(getResources().getStringArray(R.array.steps));

        for (int i = 0; i < listStepTitle.size(); i++) {
            steps.add(new Step(listStepTitle.get(i)));
        }

        stepView.setListSteps(steps, listStepTitle);
```

Supported customization:

Name| Preview
-------- | ---
`WITHOUT_CUSTUMIZATION`| ![without_cuztomization](/images/WITHOUT_CUSTOMIZATION.jpeg)
`CUSTOMIZE_STATE`| ![customize_state](/images/CUSTOMIZE_STATE.jpeg)
`CUSTUMIZE_STATE_4_AND_5`| ![customize_state_4_and_5](/images/CUSTOMIZE_STATE_4_AND_5.jpeg)

Customized the state of step ( complete or not completed ). Default state is NOT_COMPLETED.
Customized the state to complete with below code:

```java
        //customizee the state for completed step
        steps.get(2).setState(Step.State.COMPLETED);
        steps.get(4).setState(Step.State.COMPLETED);
	
	
	//or call it when go to next step
	if (currentStep < stepView.getStepCount() - 1) {
	    steps.get(currentStep).setState(Step.State.COMPLETED);
	    currentStep++;
	    stepView.go(currentStep, true);
        }
```

Styling:

```xml
<com.meylingtjan.stepview.StepView
    android:id="@+id/step_view"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:padding="16dp"
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:sv_animationType="All"
    app:sv_stepPadding="12dp"
    app:sv_typeface="@font/iran_sans_mobile"
    app:sv_stepNumberTextSize="12sp"
    app:sv_steps="@array/steps"
    app:sv_doneCircleColor="@color/stepview_circle_done"
    app:sv_doneCircleRadius="12dp"
    app:sv_doneStepLineColor="@color/stepview_line_done"
    app:sv_doneStepMarkColor="@color/stepview_mark"
    app:sv_doneTextColor="@color/stepview_text_done"
    app:sv_nextStepCircleColor="@color/stepview_line_next"
    app:sv_nextStepCircleEnabled="true"
    app:sv_nextStepLineColor="@color/stepview_line_next"
    app:sv_nextTextColor="@color/stepview_text_next"
    app:sv_selectedCircleColor="@color/stepview_circle_selected"
    app:sv_selectedCircleRadius="12dp"
    app:sv_selectedStepNumberColor="@color/stepview_selected_number"
    app:sv_selectedTextColor="@color/stepview_text_selected"
    app:sv_stepLineWidth="4dp"
    app:sv_stepViewStyle="@style/StepView"
/>
```

or instantiate and setup it in runtime with handy state builder:

```java
    stepView.getState()
            .selectedTextColor(ContextCompat.getColor(this, R.color.stepview_text_selected))
            .animationType(StepView.ANIMATION_ALL)
            .selectedCircleColor(ContextCompat.getColor(this, R.color.stepview_circle_selected))
            .selectedCircleRadius(getResources().getDimensionPixelSize(R.dimen.dp12))
            .selectedStepNumberColor(ContextCompat.getColor(this, R.color.stepview_selected_number))
	    .selectedTextColor(ContextCompat.getColor(this, R.color.stepview_text_selected))

            .doneCircleColor(ContextCompat.getColor(this, R.color.stepview_circle_done))
            .doneCircleRadius(getResources().getDimensionPixelSize(R.dimen.dp12))
            .doneStepLineColor(ContextCompat.getColor(this, R.color.stepview_line_done))
	    .doneStepMarkColor(ContextCompat.getColor(this, R.color.stepview_mark))
            .doneTextColor(ContextCompat.getColor(this, R.color.stepview_text_done))
	    
	    .nextStepLineColor(ContextCompat.getColor(this, R.color.stepview_line_next))
            .nextTextColor(ContextCompat.getColor(this, R.color.stepview_text_next))
	    .nextStepCircleEnabled="true"
	    
            .animationDuration(getResources().getInteger(android.R.integer.config_shortAnimTime))
            .stepLineWidth(getResources().getDimensionPixelSize(R.dimen.dp1))
            .stepNumberTextSize(getResources().getDimensionPixelSize(R.dimen.sp12))
            .typeface(ResourcesCompat.getFont(context, R.font.iran_sans_mobile))
            // other state methods are equal to the corresponding xml attributes
            .commit();
```

Change a step:
```java
    // Passing 'true' triggers an animation if enabled.
    // Animation would run if a difference between current and next is 1.
    stepView.go(step, true);
```

To mark last step use a done mark:
```java
	stepView.done(true);
```
To allow going back after set a done mark for last step, please unmark the done state:
```java
	stepView.done(false)
```

See the sample for additional details, to see how to set the state to the specific step.

Credits
=======

This repo is a fork of [Shuhart-StepsView](https://github.com/shuhart/StepView).
