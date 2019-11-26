- `controller-gen` v0.2.4
- `kubebuilder` v2.2.0

```
go mod init pires.github.com/example

kubebuilder init --domain pires.github.com

kubebuilder create api --group example --version v1alpha1 --kind Stuff --namespaced --resource --controller
```

Edit `api1/v1alpha/stuff_types.go` to look exactly like follows:

```go
package v1alpha1

import (
        metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
)

// EDIT THIS FILE!  THIS IS SCAFFOLDING FOR YOU TO OWN!
// NOTE: json tags are required.  Any new fields you add must have json tags for the fields to be serialized.

// StuffSpec defines the desired state of Stuff
type StuffSpec struct {
        // INSERT ADDITIONAL SPEC FIELDS - desired state of cluster
        // Important: Run "make" to regenerate code after modifying this file

        // Foo is an example field of Stuff. Edit Stuff_types.go to remove/update
        Foo string `json:"foo,omitempty"`
}

// StuffStatus defines the observed state of Stuff
type StuffStatus struct {
        // INSERT ADDITIONAL STATUS FIELD - define observed state of cluster
        // Important: Run "make" to regenerate code after modifying this file

        Phase string `json:"phase,omitempty"`
}

// +kubebuilder:object:root=true
// +kubebuilder:subresource:status
// +kubebuilder:printcolumn:name="Phase",type="string",JSONPath=".status.phase",description="stuff status"

// Stuff is the Schema for the stuffs API
type Stuff struct {
        metav1.TypeMeta   `json:",inline"`
        metav1.ObjectMeta `json:"metadata,omitempty"`

        Spec   StuffSpec   `json:"spec,omitempty"`
        Status StuffStatus `json:"status,omitempty"`
}

// +kubebuilder:object:root=true

// StuffList contains a list of Stuff
type StuffList struct {
        metav1.TypeMeta `json:",inline"`
        metav1.ListMeta `json:"metadata,omitempty"`
        Items           []Stuff `json:"items"`
}

func init() {
        SchemeBuilder.Register(&Stuff{}, &StuffList{})
}
```

Now, run:

```
make manifests
```
