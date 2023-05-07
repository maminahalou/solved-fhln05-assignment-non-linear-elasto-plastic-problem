Download Link: https://assignmentchef.com/product/solved-fhln05-assignment-non-linear-elasto-plastic-problem
<br>
<h1>Problem description</h1>

A thin steel plate should be examined as it undergoes elasto-plastic deformation. The geometry of the plate is shown in figure 1.

Figure 1: Geometry of the thin steel plate, dimensions in meter.

A uniform displacement, in the horizontal direction, is applied to the left and right boundary of the structure such that two symmetry axis are present; <em>x </em>= 100 mm and <em>y </em>= 0 mm, therefore only one quadrant of the profile is required for analysis, as depicted in Figure 2.

Figure 2: Geometry of the thin steel plate, dimensions in meter.

Referring to Figure 2 the top left small hole has a diameter of 3 mm and has its center at (30<em>, </em>9<em>.</em>5) mm. The elliptic hole has its center at (65<em>, </em>0) m and has the half-axis 20 mm along <em>x </em>and 10 mm along <em>y</em>. The half-circle has a radius of 10 mm and its center at (100<em>,</em>20) mm. The chamfering of the top right corner is 40 by 10 mm and the thickness of the profile is 1 mm.

In the development process of the plate, two different steel qualities are considered. Both qualities have the same elastic properties but they have different response to plastic deformation. The elastic modulus is <em>E </em>= 190 GPa and the Poisson’s ratio is <em>ν </em>= 0<em>.</em>3. In the elastic regime the material is considered linear and due to the small out of plane dimension plane stress is assumed, i.e, Hooke’s law for plane stress can be used.

For the plastic loading, the materials can be modelled using von Mises yield surface with isotropic hardening, where associated plasticity can be assumed. The yield stress for the materials are given by the following expressions

Material 1 :                                                       (1)

Material 2 :        <em>σ<sub>y </sub></em>= <em>σ<sub>y</sub></em><sub>0 </sub>+ <em>ασ<sub>y</sub></em><sub>0</sub>(<em>ε<sup>p</sup><sub>eff</sub></em>)<em><sup>n                                                                                                                                </sup></em>(2)

where the parameters <em>σ<sub>y</sub></em><sub>0 </sub>= 230 MPa, <em>K</em><sub>∞ </sub>= 300 MPa, <em>h </em>= 21 GPa, <em>α </em>= 17, <em>n </em>= 0<em>.</em>61 and <em>ε<sup>p</sup><sub>eff </sub></em>is the effective plastic strain.

<h1>Assignment</h1>

The task is to calculate the elasto-plastic response of a given structure. The elasto-plastic response is the solution to the equation of motion (static conditions may be assumed and body forces may be neglected). To solve the problem the CALFEM-toolbox should be used. In CALFEM, certain general FE-routines are already established but you need to establish extra routines in order to solve the elastic-plastic boundary value problem.

The routine TopConstMod_Assigmnent2021.m may be used to obtain the topology matrices and Dirichlet boundary conditions bc. Figure 2 shows the part to be meshed.

For the global equilibrium loop a Newton-Raphson scheme should be implemented and for the integration of the elasto-plastic constitutive laws a fully implicit radial return method should be used (cf. chapter 18 in the course book, note that plane stress conditions prevail!). Three-node triangle elements are used for the finite element calculations. The calculations should be carried out using the plane stress assumption.

<h1>The assignment includes the following</h1>

<ul>

 <li>Derive the FE formulation of the equation of motion.</li>

 <li>Derive the equilibrium iteration procedure by defining and linearizing a residual, i.e. Newton-Raphson procedure.</li>

 <li>Derive the numerical algorithmic tangent stiffness <strong>D<sub>ats </sub></strong>and the radial return method for isotropic hardening of von Mises yield surface.</li>

 <li>Using a simple 2 element setup (illustrated in figure A.1 in appendix) plot the force-displacement curve for the different materials during a load-cycle where the material is plastically deformed (includes loading, unloading and re-loading).</li>

 <li>Investigate the elasto-plastic response of the steel profile by implementing a FE program using the Newton-Raphson algorithm with a fully implicit radial return method using displacement controled boundary conditions. This includes:

  <ul>

   <li>Implementation of the subroutines update_variables1.m and update_variables2.m that checks for elasto-plastic response and updates accordingly (a manual for the routines is appended). The number indicate which hardening model that is considered. The routines can be checked with data from check_update_2021.mat. The subscripts 1 and 2 from the data produced by the file refers to the different hardening models.</li>

   <li>Implementation of the subroutines alg_tan_stiff1.m and alg_tan_stiff2.m that calculates the algorithmic tangent stiffness (a manual for this routine is appended) of the corresponding material. The routines can be checked with data from check_Dats_2021.mat. The subscripts 1 and 2 from the data produced by the file refers to the two material models.</li>

  </ul></li>

 <li>Use displacement controlled loading and load the structure well into the plastic region by applying a +1 mm boundary displacement. Return to the original position i.e, at boundary displacement zero.</li>

 <li>The following results should be presented in an illustrative way:

  <ul>

   <li>A force-displacement curve for a load-cycle using the simple 2-element setup. The response for both materials should be presented.</li>

   <li>The development of plastic response regions at maximum load, zero load, as well as one or more intermediate load levels for both materials.</li>

   <li>The effective von Mises stress distribution at maximum load and after unloading, for both materials.</li>

   <li>A force-displacement curve at the region of the actively applied boundary condition.</li>

  </ul></li>

</ul>

Remember that there are two different materials so the subroutines are slightly different because the materials have different hardening.

The report should be well structured and contain sufficient details of the derivations with given assumptions and approximations for the reader to understand. Furthermore, some useful hints are given in appendix.

Good luck!

Appendix A

<ul>

 <li>Variables</li>

</ul>

<table width="648">

 <tbody>

  <tr>

   <td width="80">Variable</td>

   <td width="440">Description</td>

   <td width="127">Size</td>

  </tr>

  <tr>

   <td width="80">bc</td>

   <td width="440">Dirichlet boundary conditions (value one for active boundary)</td>

   <td width="127">[nbr_bc_dofs×2]</td>

  </tr>

  <tr>

   <td width="80">coord</td>

   <td width="440">Coordinates of nodes</td>

   <td width="127">[nbr_node×2]</td>

  </tr>

  <tr>

   <td width="80">dof</td>

   <td width="440">Degrees of freedom</td>

   <td width="127">[nbr_node×2]</td>

  </tr>

  <tr>

   <td width="80">edof</td>

   <td width="440">Element topology matrix</td>

   <td width="127">[nbr_elem×7]</td>

  </tr>

  <tr>

   <td width="80">enod</td>

   <td width="440">Element nodes</td>

   <td width="127">[nbr_elem×3]</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Hints</li>

</ul>

<ul>

 <li>From <em>f </em>= <em>f</em>(σ<sup>(2)</sup><em>,K</em><sup>(2)</sup>) = 0 it is possible to derive a constraint that can be used to find the increment ∆<em>λ</em>;</li>

</ul>

PMσ<em><sup>t </sup></em><sup>− </sup><em>σ<sub>y</sub></em><sup>2 </sup>= 0                                                                    (A.1)

where <strong>P </strong>is a matrix that maps the stresses σ (for a plane stress scenario) to the deviatoric stresses <strong>s</strong>, i.e. <strong>s </strong>= <strong>P</strong>σ. Explicitly the matrix <strong>P </strong>should be as

<strong>P</strong>

Note, the report should contain a derivation of this expression in order to get maximum number of points on the assignment. Note that <strong>M </strong>also depend on ∆<em>λ</em>!

In order to solve the constraint given by equation (A.1) for ∆<em>λ </em>the command fzero in Matlab could be used.

<ul>

 <li>In order to simplify the integration of the variables, the von Mises yield condition can be written as (verify this!);</li>

</ul>

(A.2)

4) You could use a modified Newton-Raphson scheme to solve the problem, i.e. use the elastic tangent stiffness instead of <strong>D</strong><em><sub>ats</sub></em>. The convergence will then be impaired but it could be useful when developing your program. Note that for a maximum number of points on the assignment you will need to use the full Newton-Raphson.

Figure A.1: Simple two element structure with boundary conditions and loaded nodes prescribed (thickness 1 mm). Dimensions in mm.

.

<h1>alg_tan_stiff</h1>

Purpose: Compute the algorithmic tangent stiffness matrix for a triangular 3 node element under plane stress conditions for the above presented isotropic hardening model.

Syntax: Dats = alg_tan_stiff(sigma,dlambda,ep_eff,Dstar,mp)

Description: alg_tan_stiff provides the algorithmic tangent stiffness matrix Dats for a triangular 3 node element. The stress is provided by sigma = [<em>σ</em><sub>11</sub><em>, σ</em><sub>22</sub><em>, σ</em><sub>12</sub>]<em><sup>T</sup></em>. Dstar is the linear elastic material tangent for plane stress, dlambda is the increment ∆<em>λ</em>, ep_eff is the effective deviatoric plastic strain <em>ε<sup>p</sup><sub>d </sub></em>and mp a vector containing the material parameters needed.

The algorithmic tangent stiffness is defined according to equation (18.64) in the course book;

D<em>ats </em>= D

where

D

D<em><sub>⋆ </sub></em>denotes the linear elastic material tangent given by Dstar.

<h1>update_variables</h1>

Purpose: Check for elasto-plastic response and update the stress, plastic multiplier and effective plastic deviatoric strain accordingly for a triangular 3 node element under plane stress conditions for the above presented isotropic hardening model.

Syntax:

[sigma,dlambda,ep_eff] = update_variables(sigma_old,ep_eff_old,delta_eps,Dstar,mp)

Description: update_variables provides updates of the stress sigma, the increment in plastic multiplier dlambda and the effective plastic deviatoric strain ep_eff. The variables are calculated from stress and effective plastic strain at the last accepted equilibrium state sigma_old and ep_eff_old, respectively. The variable delta_eps is the increment in strains between the last equilibrium state and the current state.

The increment ∆<em>λ </em>needed to update the stresses and strains are also computed and could be used as an indicator of plasticity later on in the code and will therefore also be used as output from this function.

Moreover Dstar denotes the linear elastic material tangent for plane stress and mp is a vector containing the material parameters needed.